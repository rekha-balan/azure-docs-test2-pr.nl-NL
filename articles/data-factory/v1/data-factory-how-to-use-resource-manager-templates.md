---
title: Use Resource Manager templates in Data Factory | Microsoft Docs
description: Learn how to create and use Azure Resource Manager templates to create Data Factory entities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
editor: ''
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 3419f8718396bfb4ec894310e545f6a8a5b8f718
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857363"
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="cf0bb-103">Use templates to create Azure Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="cf0bb-103">Use templates to create Azure Data Factory entities</span></span>
> [!NOTE]
> <span data-ttu-id="cf0bb-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-104">This article applies to version 1 of Data Factory.</span></span> 

## <a name="overview"></a><span data-ttu-id="cf0bb-105">Overview</span><span class="sxs-lookup"><span data-stu-id="cf0bb-105">Overview</span></span>
<span data-ttu-id="cf0bb-106">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-106">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="cf0bb-107">Templates help you implement and manage these scenarios in an easy manner.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-107">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="cf0bb-108">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-108">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="cf0bb-109">Consider the situation where an organization has 10 manufacturing plants across the world.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-109">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="cf0bb-110">The logs from each plant are stored in a separate on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-110">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="cf0bb-111">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-111">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="cf0bb-112">It also wants to have the same logic but different configurations for development, test, and production environments.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-112">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="cf0bb-113">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-113">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="cf0bb-114">In effect, **repetition** is present.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-114">In effect, **repetition** is present.</span></span> <span data-ttu-id="cf0bb-115">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-115">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="cf0bb-116">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-116">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="cf0bb-117">Templating with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cf0bb-117">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="cf0bb-118">[Azure Resource Manager templates](../../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-118">[Azure Resource Manager templates](../../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="cf0bb-119">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-119">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="cf0bb-120">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-120">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="cf0bb-121">See [Authoring Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-121">See [Authoring Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="cf0bb-122">Tutorials</span><span class="sxs-lookup"><span data-stu-id="cf0bb-122">Tutorials</span></span>
<span data-ttu-id="cf0bb-123">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-123">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="cf0bb-124">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="cf0bb-124">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="cf0bb-125">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="cf0bb-125">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="cf0bb-126">Data Factory templates on GitHub</span><span class="sxs-lookup"><span data-stu-id="cf0bb-126">Data Factory templates on GitHub</span></span>
<span data-ttu-id="cf0bb-127">Check out the following Azure quick start templates on GitHub:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-127">Check out the following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="cf0bb-128">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cf0bb-128">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="cf0bb-129">Create a Data factory with Hive activity on Azure HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="cf0bb-129">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="cf0bb-130">Create a Data factory to copy data from Salesforce to Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="cf0bb-130">Create a Data factory to copy data from Salesforce to Azure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="cf0bb-131">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cf0bb-131">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="cf0bb-132">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="cf0bb-132">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="cf0bb-133">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-133">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="cf0bb-134">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-134">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="cf0bb-135">Defining Data Factory resources in templates</span><span class="sxs-lookup"><span data-stu-id="cf0bb-135">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="cf0bb-136">The top-level template for defining a data factory is:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-136">The top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="cf0bb-137">Define data factory</span><span class="sxs-lookup"><span data-stu-id="cf0bb-137">Define data factory</span></span>
<span data-ttu-id="cf0bb-138">You define a data factory in the Resource Manager template as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-138">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="cf0bb-139">The dataFactoryName is defined in “variables” as:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-139">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="cf0bb-140">Define linked services</span><span class="sxs-lookup"><span data-stu-id="cf0bb-140">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="cf0bb-141">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-141">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="cf0bb-142">The “dependsOn” parameter specifies name of the corresponding data factory.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-142">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="cf0bb-143">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-143">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="cf0bb-144">Define datasets</span><span class="sxs-lookup"><span data-stu-id="cf0bb-144">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="cf0bb-145">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-145">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="cf0bb-146">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-146">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="cf0bb-147">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-147">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="cf0bb-148">Define pipelines</span><span class="sxs-lookup"><span data-stu-id="cf0bb-148">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="cf0bb-149">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-149">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="cf0bb-150">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-150">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="cf0bb-151">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-151">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="cf0bb-152">Parameterizing Data Factory template</span><span class="sxs-lookup"><span data-stu-id="cf0bb-152">Parameterizing Data Factory template</span></span>
<span data-ttu-id="cf0bb-153">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../../azure-resource-manager/resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="cf0bb-153">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../../azure-resource-manager/resource-manager-template-best-practices.md).</span></span> <span data-ttu-id="cf0bb-154">In general, parameter usage should be minimized, especially if variables can be used instead.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-154">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="cf0bb-155">Only provide parameters in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-155">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="cf0bb-156">Settings vary by environment (example: development, test, and production)</span><span class="sxs-lookup"><span data-stu-id="cf0bb-156">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="cf0bb-157">Secrets (such as passwords)</span><span class="sxs-lookup"><span data-stu-id="cf0bb-157">Secrets (such as passwords)</span></span>

<span data-ttu-id="cf0bb-158">If you need to pull secrets from [Azure Key Vault](../../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="cf0bb-158">If you need to pull secrets from [Azure Key Vault](../../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="cf0bb-159">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span><span class="sxs-lookup"><span data-stu-id="cf0bb-159">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
