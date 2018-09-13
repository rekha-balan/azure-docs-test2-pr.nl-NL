---
title: Datasets and linked services in Azure Data Factory | Microsoft Docs
description: Learn about datasets and linked services in Data Factory. Linked services link compute/data stores to data factory. Datasets represent input/output data.
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
ms.date: 01/22/2018
ms.author: shlo
ms.openlocfilehash: d5cf4005ad50c9c75f22b2fa2719925afbe69f26
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968444"
---
# <a name="datasets-and-linked-services-in-azure-data-factory"></a><span data-ttu-id="1a6d3-105">Datasets and linked services in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1a6d3-105">Datasets and linked services in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-create-datasets.md)
> * [Current version](concepts-datasets-linked-services.md)

<span data-ttu-id="1a6d3-108">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-108">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> 

<span data-ttu-id="1a6d3-109">If you are new to Data Factory, see [Introduction to Azure Data Factory](introduction.md) for an overview.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-109">If you are new to Data Factory, see [Introduction to Azure Data Factory](introduction.md) for an overview.</span></span> 

## <a name="overview"></a><span data-ttu-id="1a6d3-110">Overview</span><span class="sxs-lookup"><span data-stu-id="1a6d3-110">Overview</span></span>
<span data-ttu-id="1a6d3-111">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="1a6d3-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="1a6d3-113">The activities in a pipeline define actions to perform on your data.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-113">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="1a6d3-114">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-114">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span></span> <span data-ttu-id="1a6d3-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span></span> <span data-ttu-id="1a6d3-116">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-116">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="1a6d3-117">For more information about pipelines and activities, see [Pipelines and activities](concepts-pipelines-activities.md) in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-117">For more information about pipelines and activities, see [Pipelines and activities](concepts-pipelines-activities.md) in Azure Data Factory.</span></span>

<span data-ttu-id="1a6d3-118">Now, a **dataset** is a named view of data that simply points or references the data you want to use in your **activities** as inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-118">Now, a **dataset** is a named view of data that simply points or references the data you want to use in your **activities** as inputs and outputs.</span></span> <span data-ttu-id="1a6d3-119">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-119">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="1a6d3-120">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the activity should read the data.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-120">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the activity should read the data.</span></span>

<span data-ttu-id="1a6d3-121">Before you create a dataset, you must create a **linked service** to link your data store to the data factory.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-121">Before you create a dataset, you must create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="1a6d3-122">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-122">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="1a6d3-123">Think of it this way; the dataset represents the structure of the data within the linked data stores, and the linked service defines the connection to the data source.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-123">Think of it this way; the dataset represents the structure of the data within the linked data stores, and the linked service defines the connection to the data source.</span></span> <span data-ttu-id="1a6d3-124">For example, an Azure Storage linked service links a storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-124">For example, an Azure Storage linked service links a storage account to the data factory.</span></span> <span data-ttu-id="1a6d3-125">An Azure Blob dataset represents the blob container and the folder within that Azure storage account that contains the input blobs to be processed.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-125">An Azure Blob dataset represents the blob container and the folder within that Azure storage account that contains the input blobs to be processed.</span></span>

<span data-ttu-id="1a6d3-126">Here is a sample scenario.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-126">Here is a sample scenario.</span></span> <span data-ttu-id="1a6d3-127">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-127">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="1a6d3-128">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-128">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span></span> <span data-ttu-id="1a6d3-129">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-129">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="1a6d3-130">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-130">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span></span> <span data-ttu-id="1a6d3-131">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-131">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="1a6d3-132">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-132">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span>

![Relationship between pipeline, activity, dataset, linked services](media/concepts-datasets-linked-services/relationship-between-data-factory-entities.png)

## <a name="linked-service-json"></a><span data-ttu-id="1a6d3-134">Linked service JSON</span><span class="sxs-lookup"><span data-stu-id="1a6d3-134">Linked service JSON</span></span>
<span data-ttu-id="1a6d3-135">A linked service in Data Factory is defined in JSON format as follows:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-135">A linked service in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<Name of the linked service>",
    "properties": {
        "type": "<Type of the linked service>",
        "typeProperties": {
              "<data store or compute-specific type properties>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="1a6d3-136">The following table describes properties in the above JSON:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-136">The following table describes properties in the above JSON:</span></span>

<span data-ttu-id="1a6d3-137">Property</span><span class="sxs-lookup"><span data-stu-id="1a6d3-137">Property</span></span> | <span data-ttu-id="1a6d3-138">Description</span><span class="sxs-lookup"><span data-stu-id="1a6d3-138">Description</span></span> | <span data-ttu-id="1a6d3-139">Required</span><span class="sxs-lookup"><span data-stu-id="1a6d3-139">Required</span></span> |
-------- | ----------- | -------- |
<span data-ttu-id="1a6d3-140">name</span><span class="sxs-lookup"><span data-stu-id="1a6d3-140">name</span></span> | <span data-ttu-id="1a6d3-141">Name of the linked service.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-141">Name of the linked service.</span></span> <span data-ttu-id="1a6d3-142">See [Azure Data Factory - Naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-142">See [Azure Data Factory - Naming rules](naming-rules.md).</span></span> |  <span data-ttu-id="1a6d3-143">Yes</span><span class="sxs-lookup"><span data-stu-id="1a6d3-143">Yes</span></span> |
<span data-ttu-id="1a6d3-144">type</span><span class="sxs-lookup"><span data-stu-id="1a6d3-144">type</span></span> | <span data-ttu-id="1a6d3-145">Type of the linked service.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-145">Type of the linked service.</span></span> <span data-ttu-id="1a6d3-146">For example: AzureStorage (data store) or AzureBatch (compute).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-146">For example: AzureStorage (data store) or AzureBatch (compute).</span></span> <span data-ttu-id="1a6d3-147">See the description for typeProperties.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-147">See the description for typeProperties.</span></span> | <span data-ttu-id="1a6d3-148">Yes</span><span class="sxs-lookup"><span data-stu-id="1a6d3-148">Yes</span></span> |
<span data-ttu-id="1a6d3-149">typeProperties</span><span class="sxs-lookup"><span data-stu-id="1a6d3-149">typeProperties</span></span> | <span data-ttu-id="1a6d3-150">The type properties are different for each data store or compute.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-150">The type properties are different for each data store or compute.</span></span> <br/><br/> <span data-ttu-id="1a6d3-151">For the supported data store types and their type properties, see the [dataset type](#dataset-type) table in this article.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-151">For the supported data store types and their type properties, see the [dataset type](#dataset-type) table in this article.</span></span> <span data-ttu-id="1a6d3-152">Navigate to the data store connector article to learn about type properties specific to a data store.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-152">Navigate to the data store connector article to learn about type properties specific to a data store.</span></span> <br/><br/> <span data-ttu-id="1a6d3-153">For the supported compute types and their type properties, see [Compute linked services](compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-153">For the supported compute types and their type properties, see [Compute linked services](compute-linked-services.md).</span></span> | <span data-ttu-id="1a6d3-154">Yes</span><span class="sxs-lookup"><span data-stu-id="1a6d3-154">Yes</span></span> |
<span data-ttu-id="1a6d3-155">connectVia</span><span class="sxs-lookup"><span data-stu-id="1a6d3-155">connectVia</span></span> | <span data-ttu-id="1a6d3-156">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-156">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="1a6d3-157">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in a private network).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-157">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in a private network).</span></span> <span data-ttu-id="1a6d3-158">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-158">If not specified, it uses the default Azure Integration Runtime.</span></span> | <span data-ttu-id="1a6d3-159">No</span><span class="sxs-lookup"><span data-stu-id="1a6d3-159">No</span></span>

## <a name="linked-service-example"></a><span data-ttu-id="1a6d3-160">Linked service example</span><span class="sxs-lookup"><span data-stu-id="1a6d3-160">Linked service example</span></span>
<span data-ttu-id="1a6d3-161">The following linked service is an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-161">The following linked service is an Azure Storage linked service.</span></span> <span data-ttu-id="1a6d3-162">Notice that the type is set to AzureStorage.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-162">Notice that the type is set to AzureStorage.</span></span> <span data-ttu-id="1a6d3-163">The type properties for the Azure Storage linked service include a connection string.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-163">The type properties for the Azure Storage linked service include a connection string.</span></span> <span data-ttu-id="1a6d3-164">The Data Factory service uses this connection string to connect to the data store at runtime.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-164">The Data Factory service uses this connection string to connect to the data store at runtime.</span></span> 

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-json"></a><span data-ttu-id="1a6d3-165">Dataset JSON</span><span class="sxs-lookup"><span data-stu-id="1a6d3-165">Dataset JSON</span></span>
<span data-ttu-id="1a6d3-166">A dataset in Data Factory is defined in JSON format as follows:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-166">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "linkedServiceName": {
                "referenceName": "<name of linked service>",
                 "type": "LinkedServiceReference",
        },
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        }
    }
}

```
<span data-ttu-id="1a6d3-167">The following table describes properties in the above JSON:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-167">The following table describes properties in the above JSON:</span></span>

<span data-ttu-id="1a6d3-168">Property</span><span class="sxs-lookup"><span data-stu-id="1a6d3-168">Property</span></span> | <span data-ttu-id="1a6d3-169">Description</span><span class="sxs-lookup"><span data-stu-id="1a6d3-169">Description</span></span> | <span data-ttu-id="1a6d3-170">Required</span><span class="sxs-lookup"><span data-stu-id="1a6d3-170">Required</span></span> |
-------- | ----------- | -------- |
<span data-ttu-id="1a6d3-171">name</span><span class="sxs-lookup"><span data-stu-id="1a6d3-171">name</span></span> | <span data-ttu-id="1a6d3-172">Name of the dataset.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-172">Name of the dataset.</span></span> <span data-ttu-id="1a6d3-173">See [Azure Data Factory - Naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-173">See [Azure Data Factory - Naming rules](naming-rules.md).</span></span> |  <span data-ttu-id="1a6d3-174">Yes</span><span class="sxs-lookup"><span data-stu-id="1a6d3-174">Yes</span></span> |
<span data-ttu-id="1a6d3-175">type</span><span class="sxs-lookup"><span data-stu-id="1a6d3-175">type</span></span> | <span data-ttu-id="1a6d3-176">Type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-176">Type of the dataset.</span></span> <span data-ttu-id="1a6d3-177">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-177">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="1a6d3-178">For details, see [Dataset types](#dataset-type).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-178">For details, see [Dataset types](#dataset-type).</span></span> | <span data-ttu-id="1a6d3-179">Yes</span><span class="sxs-lookup"><span data-stu-id="1a6d3-179">Yes</span></span> |
<span data-ttu-id="1a6d3-180">structure</span><span class="sxs-lookup"><span data-stu-id="1a6d3-180">structure</span></span> | <span data-ttu-id="1a6d3-181">Schema of the dataset.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-181">Schema of the dataset.</span></span> <span data-ttu-id="1a6d3-182">For details, see [Dataset structure](#dataset-structure).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-182">For details, see [Dataset structure](#dataset-structure).</span></span> | <span data-ttu-id="1a6d3-183">No</span><span class="sxs-lookup"><span data-stu-id="1a6d3-183">No</span></span> |
<span data-ttu-id="1a6d3-184">typeProperties</span><span class="sxs-lookup"><span data-stu-id="1a6d3-184">typeProperties</span></span> | <span data-ttu-id="1a6d3-185">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-185">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="1a6d3-186">For details on the supported types and their properties, see [Dataset type](#dataset-type).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-186">For details on the supported types and their properties, see [Dataset type](#dataset-type).</span></span> | <span data-ttu-id="1a6d3-187">Yes</span><span class="sxs-lookup"><span data-stu-id="1a6d3-187">Yes</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="1a6d3-188">Dataset example</span><span class="sxs-lookup"><span data-stu-id="1a6d3-188">Dataset example</span></span>
<span data-ttu-id="1a6d3-189">In the following example, the dataset represents a table named MyTable in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-189">In the following example, the dataset represents a table named MyTable in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": {
                "referenceName": "MyAzureSqlLinkedService",
                 "type": "LinkedServiceReference",
        },
        "typeProperties":
        {
            "tableName": "MyTable"
        },
    }
}

```
<span data-ttu-id="1a6d3-190">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-190">Note the following points:</span></span>

- <span data-ttu-id="1a6d3-191">type is set to AzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-191">type is set to AzureSqlTable.</span></span>
- <span data-ttu-id="1a6d3-192">tableName type property (specific to AzureSqlTable type) is set to MyTable.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-192">tableName type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
- <span data-ttu-id="1a6d3-193">linkedServiceName refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-193">linkedServiceName refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span>

## <a name="dataset-type"></a><span data-ttu-id="1a6d3-194">Dataset type</span><span class="sxs-lookup"><span data-stu-id="1a6d3-194">Dataset type</span></span>
<span data-ttu-id="1a6d3-195">There are many different types of datasets, depending on the data store you use.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-195">There are many different types of datasets, depending on the data store you use.</span></span> <span data-ttu-id="1a6d3-196">See the following table for a list of data stores supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-196">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="1a6d3-197">Click a data store to learn how to create a linked service and a dataset for that data store.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-197">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-v2-supported-data-stores](../../includes/data-factory-v2-supported-data-stores.md)]

<span data-ttu-id="1a6d3-198">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-198">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="1a6d3-199">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-199">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": {
                "referenceName": "MyAzureStorageLinkedService",
                 "type": "LinkedServiceReference",
        }, 
 
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        }
    }
}
```
## <a name="dataset-structure"></a><span data-ttu-id="1a6d3-200">Dataset structure</span><span class="sxs-lookup"><span data-stu-id="1a6d3-200">Dataset structure</span></span>
<span data-ttu-id="1a6d3-201">The **structure** section is optional.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-201">The **structure** section is optional.</span></span> <span data-ttu-id="1a6d3-202">It defines the schema of the dataset by containing a collection of names and data types of columns.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-202">It defines the schema of the dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="1a6d3-203">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-203">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span></span>

<span data-ttu-id="1a6d3-204">Each column in the structure contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-204">Each column in the structure contains the following properties:</span></span>

<span data-ttu-id="1a6d3-205">Property</span><span class="sxs-lookup"><span data-stu-id="1a6d3-205">Property</span></span> | <span data-ttu-id="1a6d3-206">Description</span><span class="sxs-lookup"><span data-stu-id="1a6d3-206">Description</span></span> | <span data-ttu-id="1a6d3-207">Required</span><span class="sxs-lookup"><span data-stu-id="1a6d3-207">Required</span></span>
-------- | ----------- | --------
<span data-ttu-id="1a6d3-208">name</span><span class="sxs-lookup"><span data-stu-id="1a6d3-208">name</span></span> | <span data-ttu-id="1a6d3-209">Name of the column.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-209">Name of the column.</span></span> | <span data-ttu-id="1a6d3-210">Yes</span><span class="sxs-lookup"><span data-stu-id="1a6d3-210">Yes</span></span>
<span data-ttu-id="1a6d3-211">type</span><span class="sxs-lookup"><span data-stu-id="1a6d3-211">type</span></span> | <span data-ttu-id="1a6d3-212">Data type of the column.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-212">Data type of the column.</span></span> <span data-ttu-id="1a6d3-213">Data Factory supports the following interim data types as allowed values: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**</span><span class="sxs-lookup"><span data-stu-id="1a6d3-213">Data Factory supports the following interim data types as allowed values: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**</span></span> | <span data-ttu-id="1a6d3-214">No</span><span class="sxs-lookup"><span data-stu-id="1a6d3-214">No</span></span>
<span data-ttu-id="1a6d3-215">culture</span><span class="sxs-lookup"><span data-stu-id="1a6d3-215">culture</span></span> | <span data-ttu-id="1a6d3-216">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-216">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="1a6d3-217">The default is `en-us`.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-217">The default is `en-us`.</span></span> | <span data-ttu-id="1a6d3-218">No</span><span class="sxs-lookup"><span data-stu-id="1a6d3-218">No</span></span>
<span data-ttu-id="1a6d3-219">format</span><span class="sxs-lookup"><span data-stu-id="1a6d3-219">format</span></span> | <span data-ttu-id="1a6d3-220">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-220">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="1a6d3-221">Refer to [Custom Date and Time Format Strings](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings) on how to format datetime.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-221">Refer to [Custom Date and Time Format Strings](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings) on how to format datetime.</span></span> | <span data-ttu-id="1a6d3-222">No</span><span class="sxs-lookup"><span data-stu-id="1a6d3-222">No</span></span>

### <a name="example"></a><span data-ttu-id="1a6d3-223">Example</span><span class="sxs-lookup"><span data-stu-id="1a6d3-223">Example</span></span>
<span data-ttu-id="1a6d3-224">In the following example, suppose the source Blob data is in CSV format and contains three columns: userid, name, and lastlogindate.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-224">In the following example, suppose the source Blob data is in CSV format and contains three columns: userid, name, and lastlogindate.</span></span> <span data-ttu-id="1a6d3-225">They are of type Int64, String, and Datetime with a custom datetime format using abbreviated French names for day of the week.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-225">They are of type Int64, String, and Datetime with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="1a6d3-226">Define the Blob dataset structure as follows along with type definitions for the columns:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-226">Define the Blob dataset structure as follows along with type definitions for the columns:</span></span>

```json
"structure":
[
    { "name": "userid", "type": "Int64"},
    { "name": "name", "type": "String"},
    { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
]
```

### <a name="guidance"></a><span data-ttu-id="1a6d3-227">Guidance</span><span class="sxs-lookup"><span data-stu-id="1a6d3-227">Guidance</span></span>

<span data-ttu-id="1a6d3-228">The following guidelines help you understand when to include structure information, and what to include in the **structure** section.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-228">The following guidelines help you understand when to include structure information, and what to include in the **structure** section.</span></span> <span data-ttu-id="1a6d3-229">Learn more on how data factory maps source data to sink and when to specify structure information from [Schema and type mapping](copy-activity-schema-and-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-229">Learn more on how data factory maps source data to sink and when to specify structure information from [Schema and type mapping](copy-activity-schema-and-type-mapping.md).</span></span>

- <span data-ttu-id="1a6d3-230">**For strong schema data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-230">**For strong schema data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span></span> <span data-ttu-id="1a6d3-231">This kind of structured data source stores data schema and type information along with the data itself.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-231">This kind of structured data source stores data schema and type information along with the data itself.</span></span> <span data-ttu-id="1a6d3-232">Examples of structured data sources include SQL Server, Oracle, and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-232">Examples of structured data sources include SQL Server, Oracle, and Azure SQL Database.</span></span><br/><br/><span data-ttu-id="1a6d3-233">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-233">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span></span>
- <span data-ttu-id="1a6d3-234">**For no/weak schema data sources e.g. text file in blob storage**, include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-234">**For no/weak schema data sources e.g. text file in blob storage**, include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span></span> <span data-ttu-id="1a6d3-235">And include structure when you want to map source columns to sink columns..</span><span class="sxs-lookup"><span data-stu-id="1a6d3-235">And include structure when you want to map source columns to sink columns..</span></span>

## <a name="create-datasets"></a><span data-ttu-id="1a6d3-236">Create datasets</span><span class="sxs-lookup"><span data-stu-id="1a6d3-236">Create datasets</span></span>
<span data-ttu-id="1a6d3-237">You can create datasets by using one of these tools or SDKs: [.NET API](quickstart-create-data-factory-dot-net.md), [PowerShell](quickstart-create-data-factory-powershell.md), [REST API](quickstart-create-data-factory-rest-api.md), Azure Resource Manager Template, and Azure portal</span><span class="sxs-lookup"><span data-stu-id="1a6d3-237">You can create datasets by using one of these tools or SDKs: [.NET API](quickstart-create-data-factory-dot-net.md), [PowerShell](quickstart-create-data-factory-powershell.md), [REST API](quickstart-create-data-factory-rest-api.md), Azure Resource Manager Template, and Azure portal</span></span>

## <a name="current-version-vs-version-1-datasets"></a><span data-ttu-id="1a6d3-238">Current version vs. version 1 datasets</span><span class="sxs-lookup"><span data-stu-id="1a6d3-238">Current version vs. version 1 datasets</span></span>

<span data-ttu-id="1a6d3-239">Here are some differences between Data Factory and Data Factory version 1 datasets:</span><span class="sxs-lookup"><span data-stu-id="1a6d3-239">Here are some differences between Data Factory and Data Factory version 1 datasets:</span></span> 

- <span data-ttu-id="1a6d3-240">The external property is not supported in the current version.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-240">The external property is not supported in the current version.</span></span> <span data-ttu-id="1a6d3-241">It's replaced by a [trigger](concepts-pipeline-execution-triggers.md).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-241">It's replaced by a [trigger](concepts-pipeline-execution-triggers.md).</span></span>
- <span data-ttu-id="1a6d3-242">The policy and availability properties are not supported in the current version.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-242">The policy and availability properties are not supported in the current version.</span></span> <span data-ttu-id="1a6d3-243">The start time for a pipeline depends on [triggers](concepts-pipeline-execution-triggers.md).</span><span class="sxs-lookup"><span data-stu-id="1a6d3-243">The start time for a pipeline depends on [triggers](concepts-pipeline-execution-triggers.md).</span></span>
- <span data-ttu-id="1a6d3-244">Scoped datasets (datasets defined in a pipeline) are not supported in the current version.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-244">Scoped datasets (datasets defined in a pipeline) are not supported in the current version.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1a6d3-245">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a6d3-245">Next steps</span></span>
<span data-ttu-id="1a6d3-246">See the following tutorial for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs.</span><span class="sxs-lookup"><span data-stu-id="1a6d3-246">See the following tutorial for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs.</span></span> 

- [<span data-ttu-id="1a6d3-247">Quickstart: create a data factory using .NET</span><span class="sxs-lookup"><span data-stu-id="1a6d3-247">Quickstart: create a data factory using .NET</span></span>](quickstart-create-data-factory-dot-net.md)
- [<span data-ttu-id="1a6d3-248">Quickstart: create a data factory using PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a6d3-248">Quickstart: create a data factory using PowerShell</span></span>](quickstart-create-data-factory-powershell.md)
- [<span data-ttu-id="1a6d3-249">Quickstart: create a data factory using REST API</span><span class="sxs-lookup"><span data-stu-id="1a6d3-249">Quickstart: create a data factory using REST API</span></span>](quickstart-create-data-factory-rest-api.md)
- <span data-ttu-id="1a6d3-250">Quickstart: create a data factory using Azure portal</span><span class="sxs-lookup"><span data-stu-id="1a6d3-250">Quickstart: create a data factory using Azure portal</span></span>
