---
title: Use Resource Manager templates in Data Factory | Microsoft Docs
description: Learn how to create and use Azure Resource Manager templates to create Data Factory entities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: ''
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2017
ms.author: shlo
ms.openlocfilehash: 2faab833724bf4bb3f3262517e1d724868f7524d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553647"
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="7c4dd-103">Use templates to create Azure Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="7c4dd-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="7c4dd-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7c4dd-104">Overview</span></span>
<span data-ttu-id="7c4dd-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="7c4dd-106">Templates help you implement and manage these scenarios in an easy manner.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="7c4dd-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="7c4dd-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="7c4dd-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="7c4dd-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="7c4dd-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="7c4dd-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="7c4dd-113">In effect, **repetition** is present.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="7c4dd-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="7c4dd-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="7c4dd-116">Templating with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7c4dd-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="7c4dd-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="7c4dd-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="7c4dd-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="7c4dd-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="7c4dd-121">Tutorials</span><span class="sxs-lookup"><span data-stu-id="7c4dd-121">Tutorials</span></span>
<span data-ttu-id="7c4dd-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="7c4dd-123">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="7c4dd-123">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="7c4dd-124">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="7c4dd-124">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="7c4dd-125">Data Factory templates on GitHub</span><span class="sxs-lookup"><span data-stu-id="7c4dd-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="7c4dd-126">Check out the following Azure quick start templates on GitHub:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-126">Check out the following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="7c4dd-127">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="7c4dd-127">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="7c4dd-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="7c4dd-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="7c4dd-129">Create a Data factory to copy data from Salesforce to Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="7c4dd-129">Create a Data factory to copy data from Salesforce to Azure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="7c4dd-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="7c4dd-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="7c4dd-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="7c4dd-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="7c4dd-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="7c4dd-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="7c4dd-134">Defining Data Factory resources in templates</span><span class="sxs-lookup"><span data-stu-id="7c4dd-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="7c4dd-135">The top-level template for defining a data factory is:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-135">The top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="7c4dd-136">Define data factory</span><span class="sxs-lookup"><span data-stu-id="7c4dd-136">Define data factory</span></span>
<span data-ttu-id="7c4dd-137">You define a data factory in the Resource Manager template as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="7c4dd-138">The dataFactoryName is defined in “variables” as:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="7c4dd-139">Define linked services</span><span class="sxs-lookup"><span data-stu-id="7c4dd-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="7c4dd-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="7c4dd-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="7c4dd-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="7c4dd-143">Define datasets</span><span class="sxs-lookup"><span data-stu-id="7c4dd-143">Define datasets</span></span>

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
<span data-ttu-id="7c4dd-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="7c4dd-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="7c4dd-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="7c4dd-147">Define pipelines</span><span class="sxs-lookup"><span data-stu-id="7c4dd-147">Define pipelines</span></span>

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

<span data-ttu-id="7c4dd-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="7c4dd-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="7c4dd-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

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
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="7c4dd-151">Parameterizing Data Factory template</span><span class="sxs-lookup"><span data-stu-id="7c4dd-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="7c4dd-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="7c4dd-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="7c4dd-154">Only provide parameters in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="7c4dd-155">Settings vary by environment (example: development, test, and production)</span><span class="sxs-lookup"><span data-stu-id="7c4dd-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="7c4dd-156">Secrets (such as passwords)</span><span class="sxs-lookup"><span data-stu-id="7c4dd-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="7c4dd-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7c4dd-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

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
> <span data-ttu-id="7c4dd-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span><span class="sxs-lookup"><span data-stu-id="7c4dd-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
