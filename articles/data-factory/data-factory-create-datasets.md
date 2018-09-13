---
title: Create Datasets in Azure Data Factory | Microsoft Docs
description: Learn how to create datasets in Azure Data Factory with examples that use properties such as offset and anchorDateTime.
keywords: create dataset, dataset example, offset example
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: shlo
ms.openlocfilehash: 3dcb85bb5d663a9b9c0e00eb4dfd1c39291d09df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553191"
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="a73f7-104">Datasets in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a73f7-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="a73f7-105">This article describes datasets in Azure Data Factory and includes examples such as offset, anchorDateTime, and offset/style databases.</span><span class="sxs-lookup"><span data-stu-id="a73f7-105">This article describes datasets in Azure Data Factory and includes examples such as offset, anchorDateTime, and offset/style databases.</span></span>

> [!NOTE]
> <span data-ttu-id="a73f7-106">If you are new to Azure Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview of Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="a73f7-106">If you are new to Azure Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview of Azure Data Factory service.</span></span> <span data-ttu-id="a73f7-107">If you do not have hands-on-experience with creating data factories, going through [data transformation tutorial](data-factory-build-your-first-pipeline.md) and/or [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) would help you understand this article better.</span><span class="sxs-lookup"><span data-stu-id="a73f7-107">If you do not have hands-on-experience with creating data factories, going through [data transformation tutorial](data-factory-build-your-first-pipeline.md) and/or [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) would help you understand this article better.</span></span> 

## <a name="overview"></a><span data-ttu-id="a73f7-108">Overview</span><span class="sxs-lookup"><span data-stu-id="a73f7-108">Overview</span></span>
<span data-ttu-id="a73f7-109">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="a73f7-109">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="a73f7-110">A **pipeline** is a logical grouping of **activities** that together perform a task.</span><span class="sxs-lookup"><span data-stu-id="a73f7-110">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="a73f7-111">The activities in a pipeline define actions to perform on your data.</span><span class="sxs-lookup"><span data-stu-id="a73f7-111">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="a73f7-112">For example, you may use a copy activity to copy data from an on-premises SQL Server to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a73f7-112">For example, you may use a copy activity to copy data from an on-premises SQL Server to an Azure Blob Storage.</span></span> <span data-ttu-id="a73f7-113">Then, use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process/transform data from the blob storage to produce output data.</span><span class="sxs-lookup"><span data-stu-id="a73f7-113">Then, use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process/transform data from the blob storage to produce output data.</span></span> <span data-ttu-id="a73f7-114">Finally, use a second copy activity to copy the output data to an Azure SQL Data Warehouse on top of which business intelligence (BI) reporting solutions are built.</span><span class="sxs-lookup"><span data-stu-id="a73f7-114">Finally, use a second copy activity to copy the output data to an Azure SQL Data Warehouse on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="a73f7-115">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="a73f7-115">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) article.</span></span>

<span data-ttu-id="a73f7-116">An activity can take zero or more input **datasets** and produce one or more output datasets.</span><span class="sxs-lookup"><span data-stu-id="a73f7-116">An activity can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="a73f7-117">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span><span class="sxs-lookup"><span data-stu-id="a73f7-117">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="a73f7-118">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span><span class="sxs-lookup"><span data-stu-id="a73f7-118">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="a73f7-119">For example, an Azure Blob dataset specifies the blob container and folder in the Azure Blob Storage from which the pipeline should read the data.</span><span class="sxs-lookup"><span data-stu-id="a73f7-119">For example, an Azure Blob dataset specifies the blob container and folder in the Azure Blob Storage from which the pipeline should read the data.</span></span> 

<span data-ttu-id="a73f7-120">Before you create a dataset, you need to create a **linked service** to link your data store to the data factory.</span><span class="sxs-lookup"><span data-stu-id="a73f7-120">Before you create a dataset, you need to create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="a73f7-121">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span><span class="sxs-lookup"><span data-stu-id="a73f7-121">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="a73f7-122">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span><span class="sxs-lookup"><span data-stu-id="a73f7-122">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="a73f7-123">For example, an Azure Storage linked service links an Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="a73f7-123">For example, an Azure Storage linked service links an Azure storage account to the data factory.</span></span> <span data-ttu-id="a73f7-124">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span><span class="sxs-lookup"><span data-stu-id="a73f7-124">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span></span> 

<span data-ttu-id="a73f7-125">Here is a sample scenario: To copy data from an Azure Blob Storage to an Azure SQL Database, you create two linked services: Azure Storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a73f7-125">Here is a sample scenario: To copy data from an Azure Blob Storage to an Azure SQL Database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="a73f7-126">Then, create two datasets: Azure Blob dataset (refers to Azure Storage linked service), Azure SQL Table dataset (refers to Azure SQL Database linked service).</span><span class="sxs-lookup"><span data-stu-id="a73f7-126">Then, create two datasets: Azure Blob dataset (refers to Azure Storage linked service), Azure SQL Table dataset (refers to Azure SQL Database linked service).</span></span> <span data-ttu-id="a73f7-127">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure storage and Azure SQL database respectively.</span><span class="sxs-lookup"><span data-stu-id="a73f7-127">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure storage and Azure SQL database respectively.</span></span> <span data-ttu-id="a73f7-128">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="a73f7-128">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Azure blob storage.</span></span> <span data-ttu-id="a73f7-129">The Azure SQL Table dataset specifies the SQL table in your Azure SQL database to which the data is to be copied.</span><span class="sxs-lookup"><span data-stu-id="a73f7-129">The Azure SQL Table dataset specifies the SQL table in your Azure SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="a73f7-130">The following diagram shows the relationship between pipeline, activity, dataset, and linked service in Data Factory:</span><span class="sxs-lookup"><span data-stu-id="a73f7-130">The following diagram shows the relationship between pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relationship between pipeline, activity, dataset, linked services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="a73f7-132">Dataset JSON</span><span class="sxs-lookup"><span data-stu-id="a73f7-132">Dataset JSON</span></span>
<span data-ttu-id="a73f7-133">A dataset in Azure Data Factory is defined in JSON format as follows:</span><span class="sxs-lookup"><span data-stu-id="a73f7-133">A dataset in Azure Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="a73f7-134">The following table describes properties in the above JSON:</span><span class="sxs-lookup"><span data-stu-id="a73f7-134">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="a73f7-135">Property</span><span class="sxs-lookup"><span data-stu-id="a73f7-135">Property</span></span> | <span data-ttu-id="a73f7-136">Description</span><span class="sxs-lookup"><span data-stu-id="a73f7-136">Description</span></span> | <span data-ttu-id="a73f7-137">Required</span><span class="sxs-lookup"><span data-stu-id="a73f7-137">Required</span></span> | <span data-ttu-id="a73f7-138">Default</span><span class="sxs-lookup"><span data-stu-id="a73f7-138">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a73f7-139">name</span><span class="sxs-lookup"><span data-stu-id="a73f7-139">name</span></span> |<span data-ttu-id="a73f7-140">Name of the dataset.</span><span class="sxs-lookup"><span data-stu-id="a73f7-140">Name of the dataset.</span></span> <span data-ttu-id="a73f7-141">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span><span class="sxs-lookup"><span data-stu-id="a73f7-141">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="a73f7-142">Yes</span><span class="sxs-lookup"><span data-stu-id="a73f7-142">Yes</span></span> |<span data-ttu-id="a73f7-143">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-143">NA</span></span> |
| <span data-ttu-id="a73f7-144">type</span><span class="sxs-lookup"><span data-stu-id="a73f7-144">type</span></span> |<span data-ttu-id="a73f7-145">Type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="a73f7-145">Type of the dataset.</span></span> <span data-ttu-id="a73f7-146">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="a73f7-146">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="a73f7-147">For details, see [Dataset Type](#Type).</span><span class="sxs-lookup"><span data-stu-id="a73f7-147">For details, see [Dataset Type](#Type).</span></span> |<span data-ttu-id="a73f7-148">Yes</span><span class="sxs-lookup"><span data-stu-id="a73f7-148">Yes</span></span> |<span data-ttu-id="a73f7-149">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-149">NA</span></span> |
| <span data-ttu-id="a73f7-150">structure</span><span class="sxs-lookup"><span data-stu-id="a73f7-150">structure</span></span> |<span data-ttu-id="a73f7-151">Schema of the dataset</span><span class="sxs-lookup"><span data-stu-id="a73f7-151">Schema of the dataset</span></span><br/><br/><span data-ttu-id="a73f7-152">For details, see [Dataset Structure](#Structure).</span><span class="sxs-lookup"><span data-stu-id="a73f7-152">For details, see [Dataset Structure](#Structure).</span></span> |<span data-ttu-id="a73f7-153">No.</span><span class="sxs-lookup"><span data-stu-id="a73f7-153">No.</span></span> |<span data-ttu-id="a73f7-154">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-154">NA</span></span> |
| <span data-ttu-id="a73f7-155">typeProperties</span><span class="sxs-lookup"><span data-stu-id="a73f7-155">typeProperties</span></span> | <span data-ttu-id="a73f7-156">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span><span class="sxs-lookup"><span data-stu-id="a73f7-156">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="a73f7-157">For details on the supported types and their properties, see [Dataset Type](#Type).</span><span class="sxs-lookup"><span data-stu-id="a73f7-157">For details on the supported types and their properties, see [Dataset Type](#Type).</span></span> |<span data-ttu-id="a73f7-158">Yes</span><span class="sxs-lookup"><span data-stu-id="a73f7-158">Yes</span></span> |<span data-ttu-id="a73f7-159">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-159">NA</span></span> |
| <span data-ttu-id="a73f7-160">external</span><span class="sxs-lookup"><span data-stu-id="a73f7-160">external</span></span> | <span data-ttu-id="a73f7-161">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span><span class="sxs-lookup"><span data-stu-id="a73f7-161">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="a73f7-162">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span><span class="sxs-lookup"><span data-stu-id="a73f7-162">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span></span> <span data-ttu-id="a73f7-163">Set this flag to true for the input dataset of the first activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="a73f7-163">Set this flag to true for the input dataset of the first activity in the pipeline.</span></span>  |<span data-ttu-id="a73f7-164">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-164">No</span></span> |<span data-ttu-id="a73f7-165">false</span><span class="sxs-lookup"><span data-stu-id="a73f7-165">false</span></span> |
| <span data-ttu-id="a73f7-166">availability</span><span class="sxs-lookup"><span data-stu-id="a73f7-166">availability</span></span> | <span data-ttu-id="a73f7-167">Defines the processing window (hourly, daily, etc.) or the slicing model for the dataset production.</span><span class="sxs-lookup"><span data-stu-id="a73f7-167">Defines the processing window (hourly, daily, etc.) or the slicing model for the dataset production.</span></span> <span data-ttu-id="a73f7-168">Each unit of data consumed and produced by an activity run is called a data slice.</span><span class="sxs-lookup"><span data-stu-id="a73f7-168">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="a73f7-169">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span><span class="sxs-lookup"><span data-stu-id="a73f7-169">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="a73f7-170">For details, see [Dataset Availability](#Availability).</span><span class="sxs-lookup"><span data-stu-id="a73f7-170">For details, see [Dataset Availability](#Availability).</span></span> <br/><br/><span data-ttu-id="a73f7-171">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span><span class="sxs-lookup"><span data-stu-id="a73f7-171">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="a73f7-172">Yes</span><span class="sxs-lookup"><span data-stu-id="a73f7-172">Yes</span></span> |<span data-ttu-id="a73f7-173">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-173">NA</span></span> |
| <span data-ttu-id="a73f7-174">policy</span><span class="sxs-lookup"><span data-stu-id="a73f7-174">policy</span></span> |<span data-ttu-id="a73f7-175">Defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="a73f7-175">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="a73f7-176">For details, see [Dataset Policy](#Policy) section.</span><span class="sxs-lookup"><span data-stu-id="a73f7-176">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="a73f7-177">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-177">No</span></span> |<span data-ttu-id="a73f7-178">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-178">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="a73f7-179">Dataset example</span><span class="sxs-lookup"><span data-stu-id="a73f7-179">Dataset example</span></span>
<span data-ttu-id="a73f7-180">In the following example, the dataset represents a table named **MyTable** in an **Azure SQL database**.</span><span class="sxs-lookup"><span data-stu-id="a73f7-180">In the following example, the dataset represents a table named **MyTable** in an **Azure SQL database**.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="a73f7-181">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="a73f7-181">Note the following points:</span></span>

* <span data-ttu-id="a73f7-182">type is set to AzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="a73f7-182">type is set to AzureSqlTable.</span></span>
* <span data-ttu-id="a73f7-183">tableName type property (specific to AzureSqlTable type) is set to MyTable.</span><span class="sxs-lookup"><span data-stu-id="a73f7-183">tableName type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
* <span data-ttu-id="a73f7-184">linkedServiceName refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span><span class="sxs-lookup"><span data-stu-id="a73f7-184">linkedServiceName refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span> 
* <span data-ttu-id="a73f7-185">availability frequency is set to Day and interval is set to 1, which means that the dataset slice is produced daily.</span><span class="sxs-lookup"><span data-stu-id="a73f7-185">availability frequency is set to Day and interval is set to 1, which means that the dataset slice is produced daily.</span></span>  

<span data-ttu-id="a73f7-186">AzureSqlLinkedService is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="a73f7-186">AzureSqlLinkedService is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="a73f7-187">In the above JSON:</span><span class="sxs-lookup"><span data-stu-id="a73f7-187">In the above JSON:</span></span>

* <span data-ttu-id="a73f7-188">type is set to AzureSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a73f7-188">type is set to AzureSqlDatabase</span></span>
* <span data-ttu-id="a73f7-189">connectionString type property specifies information to connect to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="a73f7-189">connectionString type property specifies information to connect to an Azure SQL database.</span></span>  

<span data-ttu-id="a73f7-190">As you can see, the linked service defines how to connect to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="a73f7-190">As you can see, the linked service defines how to connect to an Azure SQL database.</span></span> <span data-ttu-id="a73f7-191">The dataset defines what table is used as an input/output for the activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="a73f7-191">The dataset defines what table is used as an input/output for the activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="a73f7-192">Unless a dataset is being produced by the pipeline, it should be marked as **external**.</span><span class="sxs-lookup"><span data-stu-id="a73f7-192">Unless a dataset is being produced by the pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="a73f7-193">This setting generally applies to inputs of first activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="a73f7-193">This setting generally applies to inputs of first activity in a pipeline.</span></span>   


## <a name="Type"></a> <span data-ttu-id="a73f7-194">Dataset type</span><span class="sxs-lookup"><span data-stu-id="a73f7-194">Dataset type</span></span>
<span data-ttu-id="a73f7-195">The type of the dataset depends on the data store you use.</span><span class="sxs-lookup"><span data-stu-id="a73f7-195">The type of the dataset depends on the data store you use.</span></span> <span data-ttu-id="a73f7-196">See the following table for a list of data stores supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a73f7-196">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="a73f7-197">Click a data store to learn how to create a linked service and a dataset for that data store.</span><span class="sxs-lookup"><span data-stu-id="a73f7-197">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="a73f7-198">Data stores with \* can be on-premises or on Azure IaaS, and require you to install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span><span class="sxs-lookup"><span data-stu-id="a73f7-198">Data stores with \* can be on-premises or on Azure IaaS, and require you to install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

<span data-ttu-id="a73f7-199">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="a73f7-199">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="a73f7-200">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob** as shown in the following JSON:</span><span class="sxs-lookup"><span data-stu-id="a73f7-200">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob** as shown in the following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <a name="Structure"></a><span data-ttu-id="a73f7-201">Dataset structure</span><span class="sxs-lookup"><span data-stu-id="a73f7-201">Dataset structure</span></span>
<span data-ttu-id="a73f7-202">The **structure** section is an **optional** section that defines the schema of the dataset.</span><span class="sxs-lookup"><span data-stu-id="a73f7-202">The **structure** section is an **optional** section that defines the schema of the dataset.</span></span> <span data-ttu-id="a73f7-203">It contains a collection of names and data types of columns.</span><span class="sxs-lookup"><span data-stu-id="a73f7-203">It contains a collection of names and data types of columns.</span></span> <span data-ttu-id="a73f7-204">You use the structure section to provide type information that is used to covert types and map columns from source to destination.</span><span class="sxs-lookup"><span data-stu-id="a73f7-204">You use the structure section to provide type information that is used to covert types and map columns from source to destination.</span></span> <span data-ttu-id="a73f7-205">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span><span class="sxs-lookup"><span data-stu-id="a73f7-205">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="a73f7-206">Each column in the structure contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="a73f7-206">Each column in the structure contains the following properties:</span></span>

| <span data-ttu-id="a73f7-207">Property</span><span class="sxs-lookup"><span data-stu-id="a73f7-207">Property</span></span> | <span data-ttu-id="a73f7-208">Description</span><span class="sxs-lookup"><span data-stu-id="a73f7-208">Description</span></span> | <span data-ttu-id="a73f7-209">Required</span><span class="sxs-lookup"><span data-stu-id="a73f7-209">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a73f7-210">name</span><span class="sxs-lookup"><span data-stu-id="a73f7-210">name</span></span> |<span data-ttu-id="a73f7-211">Name of the column.</span><span class="sxs-lookup"><span data-stu-id="a73f7-211">Name of the column.</span></span> |<span data-ttu-id="a73f7-212">Yes</span><span class="sxs-lookup"><span data-stu-id="a73f7-212">Yes</span></span> |
| <span data-ttu-id="a73f7-213">type</span><span class="sxs-lookup"><span data-stu-id="a73f7-213">type</span></span> |<span data-ttu-id="a73f7-214">Data type of the column.</span><span class="sxs-lookup"><span data-stu-id="a73f7-214">Data type of the column.</span></span>  |<span data-ttu-id="a73f7-215">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-215">No</span></span> |
| <span data-ttu-id="a73f7-216">culture</span><span class="sxs-lookup"><span data-stu-id="a73f7-216">culture</span></span> |<span data-ttu-id="a73f7-217">.NET based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="a73f7-217">.NET based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="a73f7-218">Default is `en-us`.</span><span class="sxs-lookup"><span data-stu-id="a73f7-218">Default is `en-us`.</span></span> |<span data-ttu-id="a73f7-219">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-219">No</span></span> |
| <span data-ttu-id="a73f7-220">format</span><span class="sxs-lookup"><span data-stu-id="a73f7-220">format</span></span> |<span data-ttu-id="a73f7-221">Format string to be used when type is a .NET type: `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="a73f7-221">Format string to be used when type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="a73f7-222">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-222">No</span></span> |

<span data-ttu-id="a73f7-223">Use the following guidelines for when to include “structure” information and what to include in the **structure** section.</span><span class="sxs-lookup"><span data-stu-id="a73f7-223">Use the following guidelines for when to include “structure” information and what to include in the **structure** section.</span></span>

* <span data-ttu-id="a73f7-224">**For structured data sources** that store data schema and type information along with the data itself (sources like SQL Server, Oracle, Azure table), specify the “structure” section only if you want map source columns to sink columns and their names are not the same.</span><span class="sxs-lookup"><span data-stu-id="a73f7-224">**For structured data sources** that store data schema and type information along with the data itself (sources like SQL Server, Oracle, Azure table), specify the “structure” section only if you want map source columns to sink columns and their names are not the same.</span></span> 
  
    <span data-ttu-id="a73f7-225">As type information is already available for structured data sources, you should not include type information when you do include the “structure” section.</span><span class="sxs-lookup"><span data-stu-id="a73f7-225">As type information is already available for structured data sources, you should not include type information when you do include the “structure” section.</span></span>
* <span data-ttu-id="a73f7-226">**For schema on read data sources (specifically Azure blob)**, you can choose to store data without storing any schema or type information with the data.</span><span class="sxs-lookup"><span data-stu-id="a73f7-226">**For schema on read data sources (specifically Azure blob)**, you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="a73f7-227">For these types of data sources, include “structure” when you want to map source columns to sink columns (or) when the dataset is an input dataset for a copy activity and data types of source dataset need to be converted to native types for the sink.</span><span class="sxs-lookup"><span data-stu-id="a73f7-227">For these types of data sources, include “structure” when you want to map source columns to sink columns (or) when the dataset is an input dataset for a copy activity and data types of source dataset need to be converted to native types for the sink.</span></span> 
    
    <span data-ttu-id="a73f7-228">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema on read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="a73f7-228">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema on read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span>

<span data-ttu-id="a73f7-229">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span><span class="sxs-lookup"><span data-stu-id="a73f7-229">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span> 
  

## <a name="Availability"></a> <span data-ttu-id="a73f7-230">Dataset availability</span><span class="sxs-lookup"><span data-stu-id="a73f7-230">Dataset availability</span></span>
<span data-ttu-id="a73f7-231">The **availability** section in a dataset defines the processing window (hourly, daily, weekly etc.) for the dataset.</span><span class="sxs-lookup"><span data-stu-id="a73f7-231">The **availability** section in a dataset defines the processing window (hourly, daily, weekly etc.) for the dataset.</span></span> <span data-ttu-id="a73f7-232">For more information about activity windows, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span><span class="sxs-lookup"><span data-stu-id="a73f7-232">For more information about activity windows, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span>

<span data-ttu-id="a73f7-233">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span><span class="sxs-lookup"><span data-stu-id="a73f7-233">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="a73f7-234">If the pipeline has following start and end times:</span><span class="sxs-lookup"><span data-stu-id="a73f7-234">If the pipeline has following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="a73f7-235">The output dataset is produced hourly within the pipeline start and end times.</span><span class="sxs-lookup"><span data-stu-id="a73f7-235">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="a73f7-236">Therefore, five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span><span class="sxs-lookup"><span data-stu-id="a73f7-236">Therefore, five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="a73f7-237">The following table describes properties you can use in the availability section:</span><span class="sxs-lookup"><span data-stu-id="a73f7-237">The following table describes properties you can use in the availability section:</span></span>

| <span data-ttu-id="a73f7-238">Property</span><span class="sxs-lookup"><span data-stu-id="a73f7-238">Property</span></span> | <span data-ttu-id="a73f7-239">Description</span><span class="sxs-lookup"><span data-stu-id="a73f7-239">Description</span></span> | <span data-ttu-id="a73f7-240">Required</span><span class="sxs-lookup"><span data-stu-id="a73f7-240">Required</span></span> | <span data-ttu-id="a73f7-241">Default</span><span class="sxs-lookup"><span data-stu-id="a73f7-241">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a73f7-242">frequency</span><span class="sxs-lookup"><span data-stu-id="a73f7-242">frequency</span></span> |<span data-ttu-id="a73f7-243">Specifies the time unit for dataset slice production.</span><span class="sxs-lookup"><span data-stu-id="a73f7-243">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="a73f7-244"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span><span class="sxs-lookup"><span data-stu-id="a73f7-244"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="a73f7-245">Yes</span><span class="sxs-lookup"><span data-stu-id="a73f7-245">Yes</span></span> |<span data-ttu-id="a73f7-246">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-246">NA</span></span> |
| <span data-ttu-id="a73f7-247">interval</span><span class="sxs-lookup"><span data-stu-id="a73f7-247">interval</span></span> |<span data-ttu-id="a73f7-248">Specifies a multiplier for frequency</span><span class="sxs-lookup"><span data-stu-id="a73f7-248">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="a73f7-249">”Frequency x interval” determines how often the slice is produced.</span><span class="sxs-lookup"><span data-stu-id="a73f7-249">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="a73f7-250">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="a73f7-250">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="a73f7-251"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span><span class="sxs-lookup"><span data-stu-id="a73f7-251"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="a73f7-252">Yes</span><span class="sxs-lookup"><span data-stu-id="a73f7-252">Yes</span></span> |<span data-ttu-id="a73f7-253">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-253">NA</span></span> |
| <span data-ttu-id="a73f7-254">style</span><span class="sxs-lookup"><span data-stu-id="a73f7-254">style</span></span> |<span data-ttu-id="a73f7-255">Specifies whether the slice should be produced at the start/end of the interval.</span><span class="sxs-lookup"><span data-stu-id="a73f7-255">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="a73f7-256">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="a73f7-256">StartOfInterval</span></span></li><li><span data-ttu-id="a73f7-257">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="a73f7-257">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="a73f7-258">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span><span class="sxs-lookup"><span data-stu-id="a73f7-258">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="a73f7-259">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span><span class="sxs-lookup"><span data-stu-id="a73f7-259">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="a73f7-260">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span><span class="sxs-lookup"><span data-stu-id="a73f7-260">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="a73f7-261">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span><span class="sxs-lookup"><span data-stu-id="a73f7-261">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="a73f7-262">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span><span class="sxs-lookup"><span data-stu-id="a73f7-262">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="a73f7-263">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-263">No</span></span> |<span data-ttu-id="a73f7-264">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="a73f7-264">EndOfInterval</span></span> |
| <span data-ttu-id="a73f7-265">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="a73f7-265">anchorDateTime</span></span> |<span data-ttu-id="a73f7-266">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span><span class="sxs-lookup"><span data-stu-id="a73f7-266">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="a73f7-267"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span><span class="sxs-lookup"><span data-stu-id="a73f7-267"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="a73f7-268">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span><span class="sxs-lookup"><span data-stu-id="a73f7-268">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="a73f7-269">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-269">No</span></span> |<span data-ttu-id="a73f7-270">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="a73f7-270">01/01/0001</span></span> |
| <span data-ttu-id="a73f7-271">offset</span><span class="sxs-lookup"><span data-stu-id="a73f7-271">offset</span></span> |<span data-ttu-id="a73f7-272">Timespan by which the start and end of all dataset slices are shifted.</span><span class="sxs-lookup"><span data-stu-id="a73f7-272">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="a73f7-273"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span><span class="sxs-lookup"><span data-stu-id="a73f7-273"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="a73f7-274">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-274">No</span></span> |<span data-ttu-id="a73f7-275">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-275">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="a73f7-276">offset example</span><span class="sxs-lookup"><span data-stu-id="a73f7-276">offset example</span></span>
<span data-ttu-id="a73f7-277">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span><span class="sxs-lookup"><span data-stu-id="a73f7-277">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="a73f7-278">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="a73f7-278">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="a73f7-279">anchorDateTime example</span><span class="sxs-lookup"><span data-stu-id="a73f7-279">anchorDateTime example</span></span>
<span data-ttu-id="a73f7-280">In the following example, the dataset is produced once every 23 hours.</span><span class="sxs-lookup"><span data-stu-id="a73f7-280">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="a73f7-281">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span><span class="sxs-lookup"><span data-stu-id="a73f7-281">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="a73f7-282">offset/style Example</span><span class="sxs-lookup"><span data-stu-id="a73f7-282">offset/style Example</span></span>
<span data-ttu-id="a73f7-283">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="a73f7-283">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a><span data-ttu-id="a73f7-284">Dataset policy</span><span class="sxs-lookup"><span data-stu-id="a73f7-284">Dataset policy</span></span>
<span data-ttu-id="a73f7-285">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="a73f7-285">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="a73f7-286">Validation policies</span><span class="sxs-lookup"><span data-stu-id="a73f7-286">Validation policies</span></span>
| <span data-ttu-id="a73f7-287">Policy Name</span><span class="sxs-lookup"><span data-stu-id="a73f7-287">Policy Name</span></span> | <span data-ttu-id="a73f7-288">Description</span><span class="sxs-lookup"><span data-stu-id="a73f7-288">Description</span></span> | <span data-ttu-id="a73f7-289">Applied To</span><span class="sxs-lookup"><span data-stu-id="a73f7-289">Applied To</span></span> | <span data-ttu-id="a73f7-290">Required</span><span class="sxs-lookup"><span data-stu-id="a73f7-290">Required</span></span> | <span data-ttu-id="a73f7-291">Default</span><span class="sxs-lookup"><span data-stu-id="a73f7-291">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a73f7-292">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="a73f7-292">minimumSizeMB</span></span> |<span data-ttu-id="a73f7-293">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span><span class="sxs-lookup"><span data-stu-id="a73f7-293">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="a73f7-294">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a73f7-294">Azure Blob</span></span> |<span data-ttu-id="a73f7-295">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-295">No</span></span> |<span data-ttu-id="a73f7-296">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-296">NA</span></span> |
| <span data-ttu-id="a73f7-297">minimumRows</span><span class="sxs-lookup"><span data-stu-id="a73f7-297">minimumRows</span></span> |<span data-ttu-id="a73f7-298">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span><span class="sxs-lookup"><span data-stu-id="a73f7-298">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="a73f7-299">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a73f7-299">Azure SQL Database</span></span></li><li><span data-ttu-id="a73f7-300">Azure Table</span><span class="sxs-lookup"><span data-stu-id="a73f7-300">Azure Table</span></span></li></ul> |<span data-ttu-id="a73f7-301">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-301">No</span></span> |<span data-ttu-id="a73f7-302">NA</span><span class="sxs-lookup"><span data-stu-id="a73f7-302">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="a73f7-303">Examples</span><span class="sxs-lookup"><span data-stu-id="a73f7-303">Examples</span></span>
<span data-ttu-id="a73f7-304">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="a73f7-304">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="a73f7-305">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="a73f7-305">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="a73f7-306">External datasets</span><span class="sxs-lookup"><span data-stu-id="a73f7-306">External datasets</span></span>
<span data-ttu-id="a73f7-307">External datasets are the ones that are not produced by a running pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="a73f7-307">External datasets are the ones that are not produced by a running pipeline in the data factory.</span></span> <span data-ttu-id="a73f7-308">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span><span class="sxs-lookup"><span data-stu-id="a73f7-308">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span></span>

<span data-ttu-id="a73f7-309">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span><span class="sxs-lookup"><span data-stu-id="a73f7-309">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="a73f7-310">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span><span class="sxs-lookup"><span data-stu-id="a73f7-310">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="a73f7-311">Name</span><span class="sxs-lookup"><span data-stu-id="a73f7-311">Name</span></span> | <span data-ttu-id="a73f7-312">Description</span><span class="sxs-lookup"><span data-stu-id="a73f7-312">Description</span></span> | <span data-ttu-id="a73f7-313">Required</span><span class="sxs-lookup"><span data-stu-id="a73f7-313">Required</span></span> | <span data-ttu-id="a73f7-314">Default Value</span><span class="sxs-lookup"><span data-stu-id="a73f7-314">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a73f7-315">dataDelay</span><span class="sxs-lookup"><span data-stu-id="a73f7-315">dataDelay</span></span> |<span data-ttu-id="a73f7-316">Time to delay the check on the availability of the external data for the given slice.</span><span class="sxs-lookup"><span data-stu-id="a73f7-316">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="a73f7-317">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span><span class="sxs-lookup"><span data-stu-id="a73f7-317">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="a73f7-318">Only applies to the present time.</span><span class="sxs-lookup"><span data-stu-id="a73f7-318">Only applies to the present time.</span></span>  <span data-ttu-id="a73f7-319">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span><span class="sxs-lookup"><span data-stu-id="a73f7-319">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="a73f7-320">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span><span class="sxs-lookup"><span data-stu-id="a73f7-320">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="a73f7-321">Time greater than 23:59 hours need to be specified using the `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="a73f7-321">Time greater than 23:59 hours need to be specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="a73f7-322">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="a73f7-322">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="a73f7-323">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="a73f7-323">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="a73f7-324">For 1 day and 4 hours, specify 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="a73f7-324">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="a73f7-325">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-325">No</span></span> |<span data-ttu-id="a73f7-326">0</span><span class="sxs-lookup"><span data-stu-id="a73f7-326">0</span></span> |
| <span data-ttu-id="a73f7-327">retryInterval</span><span class="sxs-lookup"><span data-stu-id="a73f7-327">retryInterval</span></span> |<span data-ttu-id="a73f7-328">The wait time between a failure and the next retry attempt.</span><span class="sxs-lookup"><span data-stu-id="a73f7-328">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="a73f7-329">Applies to present time; if the previous try failed, the next try is after the retryInterval period.</span><span class="sxs-lookup"><span data-stu-id="a73f7-329">Applies to present time; if the previous try failed, the next try is after the retryInterval period.</span></span> <br/><br/><span data-ttu-id="a73f7-330">If it is 1:00pm right now, we begin the first try.</span><span class="sxs-lookup"><span data-stu-id="a73f7-330">If it is 1:00pm right now, we begin the first try.</span></span> <span data-ttu-id="a73f7-331">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02pm.</span><span class="sxs-lookup"><span data-stu-id="a73f7-331">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02pm.</span></span> <br/><br/><span data-ttu-id="a73f7-332">For slices in the past, there is no delay.</span><span class="sxs-lookup"><span data-stu-id="a73f7-332">For slices in the past, there is no delay.</span></span> <span data-ttu-id="a73f7-333">The retry happens immediately.</span><span class="sxs-lookup"><span data-stu-id="a73f7-333">The retry happens immediately.</span></span> |<span data-ttu-id="a73f7-334">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-334">No</span></span> |<span data-ttu-id="a73f7-335">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="a73f7-335">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="a73f7-336">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="a73f7-336">retryTimeout</span></span> |<span data-ttu-id="a73f7-337">The timeout for each retry attempt.</span><span class="sxs-lookup"><span data-stu-id="a73f7-337">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="a73f7-338">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="a73f7-338">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="a73f7-339">If it takes longer than 10 minutes to perform the validation, the retry times out.</span><span class="sxs-lookup"><span data-stu-id="a73f7-339">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="a73f7-340">If all attempts for the validation times out, the slice is marked as TimedOut.</span><span class="sxs-lookup"><span data-stu-id="a73f7-340">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="a73f7-341">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-341">No</span></span> |<span data-ttu-id="a73f7-342">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="a73f7-342">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="a73f7-343">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="a73f7-343">maximumRetry</span></span> |<span data-ttu-id="a73f7-344">Number of times to check for the availability of the external data.</span><span class="sxs-lookup"><span data-stu-id="a73f7-344">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="a73f7-345">The allowed maximum value is 10.</span><span class="sxs-lookup"><span data-stu-id="a73f7-345">The allowed maximum value is 10.</span></span> |<span data-ttu-id="a73f7-346">No</span><span class="sxs-lookup"><span data-stu-id="a73f7-346">No</span></span> |<span data-ttu-id="a73f7-347">3</span><span class="sxs-lookup"><span data-stu-id="a73f7-347">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="a73f7-348">Create datasets</span><span class="sxs-lookup"><span data-stu-id="a73f7-348">Create datasets</span></span>
<span data-ttu-id="a73f7-349">You can create datasets by using one of these tools or SDKs.</span><span class="sxs-lookup"><span data-stu-id="a73f7-349">You can create datasets by using one of these tools or SDKs.</span></span> 

- <span data-ttu-id="a73f7-350">Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="a73f7-350">Copy Wizard.</span></span> 
- <span data-ttu-id="a73f7-351">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a73f7-351">Azure portal</span></span>
- <span data-ttu-id="a73f7-352">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a73f7-352">Visual Studio</span></span>
- <span data-ttu-id="a73f7-353">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a73f7-353">Azure PowerShell</span></span>
- <span data-ttu-id="a73f7-354">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="a73f7-354">Azure Resource Manager template</span></span>
- <span data-ttu-id="a73f7-355">REST API</span><span class="sxs-lookup"><span data-stu-id="a73f7-355">REST API</span></span>
- <span data-ttu-id="a73f7-356">.NET API</span><span class="sxs-lookup"><span data-stu-id="a73f7-356">.NET API</span></span>

<span data-ttu-id="a73f7-357">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs.</span><span class="sxs-lookup"><span data-stu-id="a73f7-357">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs.</span></span>
 
- [<span data-ttu-id="a73f7-358">Build a pipeline with a data transformation activity</span><span class="sxs-lookup"><span data-stu-id="a73f7-358">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="a73f7-359">Build a pipeline with a data movement activity</span><span class="sxs-lookup"><span data-stu-id="a73f7-359">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="a73f7-360">Once a pipeline is created/deployed, you can manage and monitor your pipelines by using the Azure portal blades or Monitor and Manage App.</span><span class="sxs-lookup"><span data-stu-id="a73f7-360">Once a pipeline is created/deployed, you can manage and monitor your pipelines by using the Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="a73f7-361">See the following topics for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="a73f7-361">See the following topics for step-by-step instructions.</span></span> 

- <span data-ttu-id="a73f7-362">[Monitor and manage pipelines by using Azure portal blades](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="a73f7-362">[Monitor and manage pipelines by using Azure portal blades](data-factory-monitor-manage-pipelines.md).</span></span>
- [<span data-ttu-id="a73f7-363">Monitor and manage pipelines by using Monitor and Manage App</span><span class="sxs-lookup"><span data-stu-id="a73f7-363">Monitor and manage pipelines by using Monitor and Manage App</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="a73f7-364">Scoped datasets</span><span class="sxs-lookup"><span data-stu-id="a73f7-364">Scoped datasets</span></span>
<span data-ttu-id="a73f7-365">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span><span class="sxs-lookup"><span data-stu-id="a73f7-365">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span></span> <span data-ttu-id="a73f7-366">These datasets can only be used by activities within this pipeline but not by activities in other pipelines.</span><span class="sxs-lookup"><span data-stu-id="a73f7-366">These datasets can only be used by activities within this pipeline but not by activities in other pipelines.</span></span> <span data-ttu-id="a73f7-367">The following example defines a pipeline with two datasets - InputDataset-rdc and OutputDataset-rdc - to be used within the pipeline:</span><span class="sxs-lookup"><span data-stu-id="a73f7-367">The following example defines a pipeline with two datasets - InputDataset-rdc and OutputDataset-rdc - to be used within the pipeline:</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a73f7-368">Scoped datasets are supported only with one-time pipelines (pipelineMode set to OneTime).</span><span class="sxs-lookup"><span data-stu-id="a73f7-368">Scoped datasets are supported only with one-time pipelines (pipelineMode set to OneTime).</span></span> <span data-ttu-id="a73f7-369">See [Onetime pipeline](data-factory-scheduling-and-execution.md#onetime-pipeline) for details.</span><span class="sxs-lookup"><span data-stu-id="a73f7-369">See [Onetime pipeline](data-factory-scheduling-and-execution.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="a73f7-370">Next Steps</span><span class="sxs-lookup"><span data-stu-id="a73f7-370">Next Steps</span></span>
- <span data-ttu-id="a73f7-371">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="a73f7-371">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md) article.</span></span> 
- <span data-ttu-id="a73f7-372">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md) article.</span><span class="sxs-lookup"><span data-stu-id="a73f7-372">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md) article.</span></span> 
