---
title: Create datasets in Azure Data Factory | Microsoft Docs
description: Learn how to create datasets in Azure Data Factory, with examples that use properties such as offset and anchorDateTime.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: f33ff3f588dac49e295a5aa96d71557d32407e46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856332"
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="499e9-103">Datasets in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="499e9-103">Datasets in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-create-datasets.md)
> * [Version 2 (current version)](../concepts-datasets-linked-services.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Datasets in V2](../concepts-datasets-linked-services.md).

<span data-ttu-id="499e9-108">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="499e9-108">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="499e9-109">It provides details about each section (for example, structure, availability, and policy) in the dataset JSON definition.</span><span class="sxs-lookup"><span data-stu-id="499e9-109">It provides details about each section (for example, structure, availability, and policy) in the dataset JSON definition.</span></span> <span data-ttu-id="499e9-110">The article also provides examples for using the **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span><span class="sxs-lookup"><span data-stu-id="499e9-110">The article also provides examples for using the **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> If you are new to Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview. If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading the [data transformation tutorial](data-factory-build-your-first-pipeline.md) and the [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a><span data-ttu-id="499e9-113">Overview</span><span class="sxs-lookup"><span data-stu-id="499e9-113">Overview</span></span>
<span data-ttu-id="499e9-114">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="499e9-114">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="499e9-115">A **pipeline** is a logical grouping of **activities** that together perform a task.</span><span class="sxs-lookup"><span data-stu-id="499e9-115">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="499e9-116">The activities in a pipeline define actions to perform on your data.</span><span class="sxs-lookup"><span data-stu-id="499e9-116">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="499e9-117">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="499e9-117">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span></span> <span data-ttu-id="499e9-118">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span><span class="sxs-lookup"><span data-stu-id="499e9-118">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span></span> <span data-ttu-id="499e9-119">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span><span class="sxs-lookup"><span data-stu-id="499e9-119">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="499e9-120">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="499e9-120">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="499e9-121">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span><span class="sxs-lookup"><span data-stu-id="499e9-121">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="499e9-122">An input dataset represents the input for an activity in the pipeline, and an output dataset represents the output for the activity.</span><span class="sxs-lookup"><span data-stu-id="499e9-122">An input dataset represents the input for an activity in the pipeline, and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="499e9-123">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span><span class="sxs-lookup"><span data-stu-id="499e9-123">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="499e9-124">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the pipeline should read the data.</span><span class="sxs-lookup"><span data-stu-id="499e9-124">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the pipeline should read the data.</span></span> 

<span data-ttu-id="499e9-125">Before you create a dataset, create a **linked service** to link your data store to the data factory.</span><span class="sxs-lookup"><span data-stu-id="499e9-125">Before you create a dataset, create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="499e9-126">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span><span class="sxs-lookup"><span data-stu-id="499e9-126">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="499e9-127">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span><span class="sxs-lookup"><span data-stu-id="499e9-127">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="499e9-128">For example, an Azure Storage linked service links a storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="499e9-128">For example, an Azure Storage linked service links a storage account to the data factory.</span></span> <span data-ttu-id="499e9-129">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span><span class="sxs-lookup"><span data-stu-id="499e9-129">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span></span> 

<span data-ttu-id="499e9-130">Here is a sample scenario.</span><span class="sxs-lookup"><span data-stu-id="499e9-130">Here is a sample scenario.</span></span> <span data-ttu-id="499e9-131">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="499e9-131">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="499e9-132">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span><span class="sxs-lookup"><span data-stu-id="499e9-132">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span></span> <span data-ttu-id="499e9-133">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span><span class="sxs-lookup"><span data-stu-id="499e9-133">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="499e9-134">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span><span class="sxs-lookup"><span data-stu-id="499e9-134">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span></span> <span data-ttu-id="499e9-135">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span><span class="sxs-lookup"><span data-stu-id="499e9-135">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="499e9-136">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span><span class="sxs-lookup"><span data-stu-id="499e9-136">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relationship between pipeline, activity, dataset, linked services](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="499e9-138">Dataset JSON</span><span class="sxs-lookup"><span data-stu-id="499e9-138">Dataset JSON</span></span>
<span data-ttu-id="499e9-139">A dataset in Data Factory is defined in JSON format as follows:</span><span class="sxs-lookup"><span data-stu-id="499e9-139">A dataset in Data Factory is defined in JSON format as follows:</span></span>

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

<span data-ttu-id="499e9-140">The following table describes properties in the above JSON:</span><span class="sxs-lookup"><span data-stu-id="499e9-140">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="499e9-141">Property</span><span class="sxs-lookup"><span data-stu-id="499e9-141">Property</span></span> | <span data-ttu-id="499e9-142">Description</span><span class="sxs-lookup"><span data-stu-id="499e9-142">Description</span></span> | <span data-ttu-id="499e9-143">Required</span><span class="sxs-lookup"><span data-stu-id="499e9-143">Required</span></span> | <span data-ttu-id="499e9-144">Default</span><span class="sxs-lookup"><span data-stu-id="499e9-144">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="499e9-145">name</span><span class="sxs-lookup"><span data-stu-id="499e9-145">name</span></span> |<span data-ttu-id="499e9-146">Name of the dataset.</span><span class="sxs-lookup"><span data-stu-id="499e9-146">Name of the dataset.</span></span> <span data-ttu-id="499e9-147">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span><span class="sxs-lookup"><span data-stu-id="499e9-147">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="499e9-148">Yes</span><span class="sxs-lookup"><span data-stu-id="499e9-148">Yes</span></span> |<span data-ttu-id="499e9-149">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-149">NA</span></span> |
| <span data-ttu-id="499e9-150">type</span><span class="sxs-lookup"><span data-stu-id="499e9-150">type</span></span> |<span data-ttu-id="499e9-151">Type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="499e9-151">Type of the dataset.</span></span> <span data-ttu-id="499e9-152">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="499e9-152">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="499e9-153">For details, see [Dataset type](#Type).</span><span class="sxs-lookup"><span data-stu-id="499e9-153">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="499e9-154">Yes</span><span class="sxs-lookup"><span data-stu-id="499e9-154">Yes</span></span> |<span data-ttu-id="499e9-155">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-155">NA</span></span> |
| <span data-ttu-id="499e9-156">structure</span><span class="sxs-lookup"><span data-stu-id="499e9-156">structure</span></span> |<span data-ttu-id="499e9-157">Schema of the dataset.</span><span class="sxs-lookup"><span data-stu-id="499e9-157">Schema of the dataset.</span></span><br/><br/><span data-ttu-id="499e9-158">For details, see [Dataset structure](#Structure).</span><span class="sxs-lookup"><span data-stu-id="499e9-158">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="499e9-159">No</span><span class="sxs-lookup"><span data-stu-id="499e9-159">No</span></span> |<span data-ttu-id="499e9-160">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-160">NA</span></span> |
| <span data-ttu-id="499e9-161">typeProperties</span><span class="sxs-lookup"><span data-stu-id="499e9-161">typeProperties</span></span> | <span data-ttu-id="499e9-162">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span><span class="sxs-lookup"><span data-stu-id="499e9-162">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="499e9-163">For details on the supported types and their properties, see [Dataset type](#Type).</span><span class="sxs-lookup"><span data-stu-id="499e9-163">For details on the supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="499e9-164">Yes</span><span class="sxs-lookup"><span data-stu-id="499e9-164">Yes</span></span> |<span data-ttu-id="499e9-165">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-165">NA</span></span> |
| <span data-ttu-id="499e9-166">external</span><span class="sxs-lookup"><span data-stu-id="499e9-166">external</span></span> | <span data-ttu-id="499e9-167">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span><span class="sxs-lookup"><span data-stu-id="499e9-167">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="499e9-168">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span><span class="sxs-lookup"><span data-stu-id="499e9-168">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span></span> <span data-ttu-id="499e9-169">Set this flag to true for the input dataset of the first activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="499e9-169">Set this flag to true for the input dataset of the first activity in the pipeline.</span></span>  |<span data-ttu-id="499e9-170">No</span><span class="sxs-lookup"><span data-stu-id="499e9-170">No</span></span> |<span data-ttu-id="499e9-171">false</span><span class="sxs-lookup"><span data-stu-id="499e9-171">false</span></span> |
| <span data-ttu-id="499e9-172">availability</span><span class="sxs-lookup"><span data-stu-id="499e9-172">availability</span></span> | <span data-ttu-id="499e9-173">Defines the processing window (for example, hourly or daily) or the slicing model for the dataset production.</span><span class="sxs-lookup"><span data-stu-id="499e9-173">Defines the processing window (for example, hourly or daily) or the slicing model for the dataset production.</span></span> <span data-ttu-id="499e9-174">Each unit of data consumed and produced by an activity run is called a data slice.</span><span class="sxs-lookup"><span data-stu-id="499e9-174">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="499e9-175">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span><span class="sxs-lookup"><span data-stu-id="499e9-175">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="499e9-176">For details, see [Dataset availability](#Availability).</span><span class="sxs-lookup"><span data-stu-id="499e9-176">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="499e9-177">For details on the dataset slicing model, see the [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span><span class="sxs-lookup"><span data-stu-id="499e9-177">For details on the dataset slicing model, see the [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="499e9-178">Yes</span><span class="sxs-lookup"><span data-stu-id="499e9-178">Yes</span></span> |<span data-ttu-id="499e9-179">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-179">NA</span></span> |
| <span data-ttu-id="499e9-180">policy</span><span class="sxs-lookup"><span data-stu-id="499e9-180">policy</span></span> |<span data-ttu-id="499e9-181">Defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="499e9-181">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="499e9-182">For details, see the [Dataset policy](#Policy) section.</span><span class="sxs-lookup"><span data-stu-id="499e9-182">For details, see the [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="499e9-183">No</span><span class="sxs-lookup"><span data-stu-id="499e9-183">No</span></span> |<span data-ttu-id="499e9-184">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-184">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="499e9-185">Dataset example</span><span class="sxs-lookup"><span data-stu-id="499e9-185">Dataset example</span></span>
<span data-ttu-id="499e9-186">In the following example, the dataset represents a table named **MyTable** in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="499e9-186">In the following example, the dataset represents a table named **MyTable** in a SQL database.</span></span>

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

<span data-ttu-id="499e9-187">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="499e9-187">Note the following points:</span></span>

* <span data-ttu-id="499e9-188">**type** is set to AzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="499e9-188">**type** is set to AzureSqlTable.</span></span>
* <span data-ttu-id="499e9-189">**tableName** type property (specific to AzureSqlTable type) is set to MyTable.</span><span class="sxs-lookup"><span data-stu-id="499e9-189">**tableName** type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
* <span data-ttu-id="499e9-190">**linkedServiceName** refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span><span class="sxs-lookup"><span data-stu-id="499e9-190">**linkedServiceName** refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span> 
* <span data-ttu-id="499e9-191">**availability frequency** is set to Day, and **interval** is set to 1.</span><span class="sxs-lookup"><span data-stu-id="499e9-191">**availability frequency** is set to Day, and **interval** is set to 1.</span></span> <span data-ttu-id="499e9-192">This means that the dataset slice is produced daily.</span><span class="sxs-lookup"><span data-stu-id="499e9-192">This means that the dataset slice is produced daily.</span></span>  

<span data-ttu-id="499e9-193">**AzureSqlLinkedService** is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="499e9-193">**AzureSqlLinkedService** is defined as follows:</span></span>

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

<span data-ttu-id="499e9-194">In the preceding JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="499e9-194">In the preceding JSON snippet:</span></span>

* <span data-ttu-id="499e9-195">**type** is set to AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="499e9-195">**type** is set to AzureSqlDatabase.</span></span>
* <span data-ttu-id="499e9-196">**connectionString** type property specifies information to connect to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="499e9-196">**connectionString** type property specifies information to connect to a SQL database.</span></span>  

<span data-ttu-id="499e9-197">As you can see, the linked service defines how to connect to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="499e9-197">As you can see, the linked service defines how to connect to a SQL database.</span></span> <span data-ttu-id="499e9-198">The dataset defines what table is used as an input and output for the activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="499e9-198">The dataset defines what table is used as an input and output for the activity in a pipeline.</span></span>   

> [!IMPORTANT]
> Unless a dataset is being produced by the pipeline, it should be marked as **external**. This setting generally applies to inputs of first activity in a pipeline.   


## <a name="Type"></a> <span data-ttu-id="499e9-201">Dataset type</span><span class="sxs-lookup"><span data-stu-id="499e9-201">Dataset type</span></span>
<span data-ttu-id="499e9-202">The type of the dataset depends on the data store you use.</span><span class="sxs-lookup"><span data-stu-id="499e9-202">The type of the dataset depends on the data store you use.</span></span> <span data-ttu-id="499e9-203">See the following table for a list of data stores supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="499e9-203">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="499e9-204">Click a data store to learn how to create a linked service and a dataset for that data store.</span><span class="sxs-lookup"><span data-stu-id="499e9-204">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS). These data stores require you to install [Data Management Gateway](data-factory-data-management-gateway.md).

<span data-ttu-id="499e9-207">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="499e9-207">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="499e9-208">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span><span class="sxs-lookup"><span data-stu-id="499e9-208">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span></span>

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

## <a name="Structure"></a><span data-ttu-id="499e9-209">Dataset structure</span><span class="sxs-lookup"><span data-stu-id="499e9-209">Dataset structure</span></span>
<span data-ttu-id="499e9-210">The **structure** section is optional.</span><span class="sxs-lookup"><span data-stu-id="499e9-210">The **structure** section is optional.</span></span> <span data-ttu-id="499e9-211">It defines the schema of the dataset by containing a collection of names and data types of columns.</span><span class="sxs-lookup"><span data-stu-id="499e9-211">It defines the schema of the dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="499e9-212">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span><span class="sxs-lookup"><span data-stu-id="499e9-212">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span></span> <span data-ttu-id="499e9-213">In the following example, the dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="499e9-213">In the following example, the dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="499e9-214">They are of type String, String, and Decimal, respectively.</span><span class="sxs-lookup"><span data-stu-id="499e9-214">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="499e9-215">Each column in the structure contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="499e9-215">Each column in the structure contains the following properties:</span></span>

| <span data-ttu-id="499e9-216">Property</span><span class="sxs-lookup"><span data-stu-id="499e9-216">Property</span></span> | <span data-ttu-id="499e9-217">Description</span><span class="sxs-lookup"><span data-stu-id="499e9-217">Description</span></span> | <span data-ttu-id="499e9-218">Required</span><span class="sxs-lookup"><span data-stu-id="499e9-218">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="499e9-219">name</span><span class="sxs-lookup"><span data-stu-id="499e9-219">name</span></span> |<span data-ttu-id="499e9-220">Name of the column.</span><span class="sxs-lookup"><span data-stu-id="499e9-220">Name of the column.</span></span> |<span data-ttu-id="499e9-221">Yes</span><span class="sxs-lookup"><span data-stu-id="499e9-221">Yes</span></span> |
| <span data-ttu-id="499e9-222">type</span><span class="sxs-lookup"><span data-stu-id="499e9-222">type</span></span> |<span data-ttu-id="499e9-223">Data type of the column.</span><span class="sxs-lookup"><span data-stu-id="499e9-223">Data type of the column.</span></span>  |<span data-ttu-id="499e9-224">No</span><span class="sxs-lookup"><span data-stu-id="499e9-224">No</span></span> |
| <span data-ttu-id="499e9-225">culture</span><span class="sxs-lookup"><span data-stu-id="499e9-225">culture</span></span> |<span data-ttu-id="499e9-226">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="499e9-226">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="499e9-227">The default is `en-us`.</span><span class="sxs-lookup"><span data-stu-id="499e9-227">The default is `en-us`.</span></span> |<span data-ttu-id="499e9-228">No</span><span class="sxs-lookup"><span data-stu-id="499e9-228">No</span></span> |
| <span data-ttu-id="499e9-229">format</span><span class="sxs-lookup"><span data-stu-id="499e9-229">format</span></span> |<span data-ttu-id="499e9-230">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="499e9-230">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="499e9-231">No</span><span class="sxs-lookup"><span data-stu-id="499e9-231">No</span></span> |

<span data-ttu-id="499e9-232">The following guidelines help you determine when to include structure information, and what to include in the **structure** section.</span><span class="sxs-lookup"><span data-stu-id="499e9-232">The following guidelines help you determine when to include structure information, and what to include in the **structure** section.</span></span>

* <span data-ttu-id="499e9-233">**For structured data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span><span class="sxs-lookup"><span data-stu-id="499e9-233">**For structured data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span></span> <span data-ttu-id="499e9-234">This kind of structured data source stores data schema and type information along with the data itself.</span><span class="sxs-lookup"><span data-stu-id="499e9-234">This kind of structured data source stores data schema and type information along with the data itself.</span></span> <span data-ttu-id="499e9-235">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span><span class="sxs-lookup"><span data-stu-id="499e9-235">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="499e9-236">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span><span class="sxs-lookup"><span data-stu-id="499e9-236">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span></span>
* <span data-ttu-id="499e9-237">**For schema on read data sources (specifically Blob storage)**, you can choose to store data without storing any schema or type information with the data.</span><span class="sxs-lookup"><span data-stu-id="499e9-237">**For schema on read data sources (specifically Blob storage)**, you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="499e9-238">For these types of data sources, include structure when you want to map source columns to sink columns.</span><span class="sxs-lookup"><span data-stu-id="499e9-238">For these types of data sources, include structure when you want to map source columns to sink columns.</span></span> <span data-ttu-id="499e9-239">Also include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span><span class="sxs-lookup"><span data-stu-id="499e9-239">Also include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span></span> 
    
    <span data-ttu-id="499e9-240">Data Factory supports the following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span><span class="sxs-lookup"><span data-stu-id="499e9-240">Data Factory supports the following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="499e9-241">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span><span class="sxs-lookup"><span data-stu-id="499e9-241">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="499e9-242">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span><span class="sxs-lookup"><span data-stu-id="499e9-242">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="499e9-243">Dataset availability</span><span class="sxs-lookup"><span data-stu-id="499e9-243">Dataset availability</span></span>
<span data-ttu-id="499e9-244">The **availability** section in a dataset defines the processing window (for example, hourly, daily, or weekly) for the dataset.</span><span class="sxs-lookup"><span data-stu-id="499e9-244">The **availability** section in a dataset defines the processing window (for example, hourly, daily, or weekly) for the dataset.</span></span> <span data-ttu-id="499e9-245">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="499e9-245">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="499e9-246">The following availability section specifies that the output dataset is either produced hourly, or the input dataset is available hourly:</span><span class="sxs-lookup"><span data-stu-id="499e9-246">The following availability section specifies that the output dataset is either produced hourly, or the input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="499e9-247">If the pipeline has the following start and end times:</span><span class="sxs-lookup"><span data-stu-id="499e9-247">If the pipeline has the following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="499e9-248">The output dataset is produced hourly within the pipeline start and end times.</span><span class="sxs-lookup"><span data-stu-id="499e9-248">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="499e9-249">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span><span class="sxs-lookup"><span data-stu-id="499e9-249">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="499e9-250">The following table describes properties you can use in the availability section:</span><span class="sxs-lookup"><span data-stu-id="499e9-250">The following table describes properties you can use in the availability section:</span></span>

| <span data-ttu-id="499e9-251">Property</span><span class="sxs-lookup"><span data-stu-id="499e9-251">Property</span></span> | <span data-ttu-id="499e9-252">Description</span><span class="sxs-lookup"><span data-stu-id="499e9-252">Description</span></span> | <span data-ttu-id="499e9-253">Required</span><span class="sxs-lookup"><span data-stu-id="499e9-253">Required</span></span> | <span data-ttu-id="499e9-254">Default</span><span class="sxs-lookup"><span data-stu-id="499e9-254">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="499e9-255">frequency</span><span class="sxs-lookup"><span data-stu-id="499e9-255">frequency</span></span> |<span data-ttu-id="499e9-256">Specifies the time unit for dataset slice production.</span><span class="sxs-lookup"><span data-stu-id="499e9-256">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="499e9-257"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span><span class="sxs-lookup"><span data-stu-id="499e9-257"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="499e9-258">Yes</span><span class="sxs-lookup"><span data-stu-id="499e9-258">Yes</span></span> |<span data-ttu-id="499e9-259">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-259">NA</span></span> |
| <span data-ttu-id="499e9-260">interval</span><span class="sxs-lookup"><span data-stu-id="499e9-260">interval</span></span> |<span data-ttu-id="499e9-261">Specifies a multiplier for frequency.</span><span class="sxs-lookup"><span data-stu-id="499e9-261">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="499e9-262">"Frequency x interval" determines how often the slice is produced.</span><span class="sxs-lookup"><span data-stu-id="499e9-262">"Frequency x interval" determines how often the slice is produced.</span></span> <span data-ttu-id="499e9-263">For example, if you need the dataset to be sliced on an hourly basis, you set <b>frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="499e9-263">For example, if you need the dataset to be sliced on an hourly basis, you set <b>frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="499e9-264">Note that if you specify **frequency** as **Minute**, you should set the interval to no less than 15.</span><span class="sxs-lookup"><span data-stu-id="499e9-264">Note that if you specify **frequency** as **Minute**, you should set the interval to no less than 15.</span></span> |<span data-ttu-id="499e9-265">Yes</span><span class="sxs-lookup"><span data-stu-id="499e9-265">Yes</span></span> |<span data-ttu-id="499e9-266">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-266">NA</span></span> |
| <span data-ttu-id="499e9-267">style</span><span class="sxs-lookup"><span data-stu-id="499e9-267">style</span></span> |<span data-ttu-id="499e9-268">Specifies whether the slice should be produced at the start or end of the interval.</span><span class="sxs-lookup"><span data-stu-id="499e9-268">Specifies whether the slice should be produced at the start or end of the interval.</span></span><ul><li><span data-ttu-id="499e9-269">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="499e9-269">StartOfInterval</span></span></li><li><span data-ttu-id="499e9-270">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="499e9-270">EndOfInterval</span></span></li></ul><span data-ttu-id="499e9-271">If **frequency** is set to **Month**, and **style** is set to **EndOfInterval**, the slice is produced on the last day of month.</span><span class="sxs-lookup"><span data-stu-id="499e9-271">If **frequency** is set to **Month**, and **style** is set to **EndOfInterval**, the slice is produced on the last day of month.</span></span> <span data-ttu-id="499e9-272">If **style** is set to **StartOfInterval**, the slice is produced on the first day of month.</span><span class="sxs-lookup"><span data-stu-id="499e9-272">If **style** is set to **StartOfInterval**, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="499e9-273">If **frequency** is set to **Day**, and **style** is set to **EndOfInterval**, the slice is produced in the last hour of the day.</span><span class="sxs-lookup"><span data-stu-id="499e9-273">If **frequency** is set to **Day**, and **style** is set to **EndOfInterval**, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="499e9-274">If **frequency** is set to **Hour**, and **style** is set to **EndOfInterval**, the slice is produced at the end of the hour.</span><span class="sxs-lookup"><span data-stu-id="499e9-274">If **frequency** is set to **Hour**, and **style** is set to **EndOfInterval**, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="499e9-275">For example, for a slice for the 1 PM - 2 PM period, the slice is produced at 2 PM.</span><span class="sxs-lookup"><span data-stu-id="499e9-275">For example, for a slice for the 1 PM - 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="499e9-276">No</span><span class="sxs-lookup"><span data-stu-id="499e9-276">No</span></span> |<span data-ttu-id="499e9-277">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="499e9-277">EndOfInterval</span></span> |
| <span data-ttu-id="499e9-278">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="499e9-278">anchorDateTime</span></span> |<span data-ttu-id="499e9-279">Defines the absolute position in time used by the scheduler to compute dataset slice boundaries.</span><span class="sxs-lookup"><span data-stu-id="499e9-279">Defines the absolute position in time used by the scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="499e9-280">Note that if this propoerty has date parts that are more granular than the specified frequency, the more granular parts are ignored.</span><span class="sxs-lookup"><span data-stu-id="499e9-280">Note that if this propoerty has date parts that are more granular than the specified frequency, the more granular parts are ignored.</span></span> <span data-ttu-id="499e9-281">For example, if the **interval** is **hourly** (frequency: hour and interval: 1), and the **anchorDateTime** contains **minutes and seconds**, then the minutes and seconds parts of **anchorDateTime** are ignored.</span><span class="sxs-lookup"><span data-stu-id="499e9-281">For example, if the **interval** is **hourly** (frequency: hour and interval: 1), and the **anchorDateTime** contains **minutes and seconds**, then the minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="499e9-282">No</span><span class="sxs-lookup"><span data-stu-id="499e9-282">No</span></span> |<span data-ttu-id="499e9-283">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="499e9-283">01/01/0001</span></span> |
| <span data-ttu-id="499e9-284">offset</span><span class="sxs-lookup"><span data-stu-id="499e9-284">offset</span></span> |<span data-ttu-id="499e9-285">Timespan by which the start and end of all dataset slices are shifted.</span><span class="sxs-lookup"><span data-stu-id="499e9-285">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="499e9-286">Note that if both **anchorDateTime** and **offset** are specified, the result is the combined shift.</span><span class="sxs-lookup"><span data-stu-id="499e9-286">Note that if both **anchorDateTime** and **offset** are specified, the result is the combined shift.</span></span> |<span data-ttu-id="499e9-287">No</span><span class="sxs-lookup"><span data-stu-id="499e9-287">No</span></span> |<span data-ttu-id="499e9-288">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-288">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="499e9-289">offset example</span><span class="sxs-lookup"><span data-stu-id="499e9-289">offset example</span></span>
<span data-ttu-id="499e9-290">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="499e9-290">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="499e9-291">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="499e9-291">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="499e9-292">anchorDateTime example</span><span class="sxs-lookup"><span data-stu-id="499e9-292">anchorDateTime example</span></span>
<span data-ttu-id="499e9-293">In the following example, the dataset is produced once every 23 hours.</span><span class="sxs-lookup"><span data-stu-id="499e9-293">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="499e9-294">The first slice starts at the time specified by **anchorDateTime**, which is set to `2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="499e9-294">The first slice starts at the time specified by **anchorDateTime**, which is set to `2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="499e9-295">offset/style example</span><span class="sxs-lookup"><span data-stu-id="499e9-295">offset/style example</span></span>
<span data-ttu-id="499e9-296">The following dataset is monthly, and is produced on the 3rd of every month at 8:00 AM (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="499e9-296">The following dataset is monthly, and is produced on the 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a><span data-ttu-id="499e9-297">Dataset policy</span><span class="sxs-lookup"><span data-stu-id="499e9-297">Dataset policy</span></span>
<span data-ttu-id="499e9-298">The **policy** section in the dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="499e9-298">The **policy** section in the dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="499e9-299">Validation policies</span><span class="sxs-lookup"><span data-stu-id="499e9-299">Validation policies</span></span>
| <span data-ttu-id="499e9-300">Policy name</span><span class="sxs-lookup"><span data-stu-id="499e9-300">Policy name</span></span> | <span data-ttu-id="499e9-301">Description</span><span class="sxs-lookup"><span data-stu-id="499e9-301">Description</span></span> | <span data-ttu-id="499e9-302">Applied to</span><span class="sxs-lookup"><span data-stu-id="499e9-302">Applied to</span></span> | <span data-ttu-id="499e9-303">Required</span><span class="sxs-lookup"><span data-stu-id="499e9-303">Required</span></span> | <span data-ttu-id="499e9-304">Default</span><span class="sxs-lookup"><span data-stu-id="499e9-304">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="499e9-305">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="499e9-305">minimumSizeMB</span></span> |<span data-ttu-id="499e9-306">Validates that the data in **Azure Blob storage** meets the minimum size requirements (in megabytes).</span><span class="sxs-lookup"><span data-stu-id="499e9-306">Validates that the data in **Azure Blob storage** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="499e9-307">Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="499e9-307">Azure Blob storage</span></span> |<span data-ttu-id="499e9-308">No</span><span class="sxs-lookup"><span data-stu-id="499e9-308">No</span></span> |<span data-ttu-id="499e9-309">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-309">NA</span></span> |
| <span data-ttu-id="499e9-310">minimumRows</span><span class="sxs-lookup"><span data-stu-id="499e9-310">minimumRows</span></span> |<span data-ttu-id="499e9-311">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span><span class="sxs-lookup"><span data-stu-id="499e9-311">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="499e9-312">Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="499e9-312">Azure SQL database</span></span></li><li><span data-ttu-id="499e9-313">Azure table</span><span class="sxs-lookup"><span data-stu-id="499e9-313">Azure table</span></span></li></ul> |<span data-ttu-id="499e9-314">No</span><span class="sxs-lookup"><span data-stu-id="499e9-314">No</span></span> |<span data-ttu-id="499e9-315">NA</span><span class="sxs-lookup"><span data-stu-id="499e9-315">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="499e9-316">Examples</span><span class="sxs-lookup"><span data-stu-id="499e9-316">Examples</span></span>
<span data-ttu-id="499e9-317">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="499e9-317">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="499e9-318">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="499e9-318">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="499e9-319">External datasets</span><span class="sxs-lookup"><span data-stu-id="499e9-319">External datasets</span></span>
<span data-ttu-id="499e9-320">External datasets are the ones that are not produced by a running pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="499e9-320">External datasets are the ones that are not produced by a running pipeline in the data factory.</span></span> <span data-ttu-id="499e9-321">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span><span class="sxs-lookup"><span data-stu-id="499e9-321">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span></span>

<span data-ttu-id="499e9-322">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span><span class="sxs-lookup"><span data-stu-id="499e9-322">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="499e9-323">This setting generally applies to the inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span><span class="sxs-lookup"><span data-stu-id="499e9-323">This setting generally applies to the inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="499e9-324">Name</span><span class="sxs-lookup"><span data-stu-id="499e9-324">Name</span></span> | <span data-ttu-id="499e9-325">Description</span><span class="sxs-lookup"><span data-stu-id="499e9-325">Description</span></span> | <span data-ttu-id="499e9-326">Required</span><span class="sxs-lookup"><span data-stu-id="499e9-326">Required</span></span> | <span data-ttu-id="499e9-327">Default value</span><span class="sxs-lookup"><span data-stu-id="499e9-327">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="499e9-328">dataDelay</span><span class="sxs-lookup"><span data-stu-id="499e9-328">dataDelay</span></span> |<span data-ttu-id="499e9-329">The time to delay the check on the availability of the external data for the given slice.</span><span class="sxs-lookup"><span data-stu-id="499e9-329">The time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="499e9-330">For example, you can delay an hourly check by using this setting.</span><span class="sxs-lookup"><span data-stu-id="499e9-330">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="499e9-331">The setting only applies to the present time.</span><span class="sxs-lookup"><span data-stu-id="499e9-331">The setting only applies to the present time.</span></span>  <span data-ttu-id="499e9-332">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span><span class="sxs-lookup"><span data-stu-id="499e9-332">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="499e9-333">Note that this setting does not affect slices in the past.</span><span class="sxs-lookup"><span data-stu-id="499e9-333">Note that this setting does not affect slices in the past.</span></span> <span data-ttu-id="499e9-334">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span><span class="sxs-lookup"><span data-stu-id="499e9-334">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="499e9-335">Times greater than 23:59 hours should be specified by using the `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="499e9-335">Times greater than 23:59 hours should be specified by using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="499e9-336">For example, to specify 24 hours, don't use 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="499e9-336">For example, to specify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="499e9-337">Instead, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="499e9-337">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="499e9-338">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="499e9-338">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="499e9-339">For 1 day and 4 hours, specify 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="499e9-339">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="499e9-340">No</span><span class="sxs-lookup"><span data-stu-id="499e9-340">No</span></span> |<span data-ttu-id="499e9-341">0</span><span class="sxs-lookup"><span data-stu-id="499e9-341">0</span></span> |
| <span data-ttu-id="499e9-342">retryInterval</span><span class="sxs-lookup"><span data-stu-id="499e9-342">retryInterval</span></span> |<span data-ttu-id="499e9-343">The wait time between a failure and the next attempt.</span><span class="sxs-lookup"><span data-stu-id="499e9-343">The wait time between a failure and the next attempt.</span></span> <span data-ttu-id="499e9-344">This setting applies to present time.</span><span class="sxs-lookup"><span data-stu-id="499e9-344">This setting applies to present time.</span></span> <span data-ttu-id="499e9-345">If the previous try failed, the next try is after the **retryInterval** period.</span><span class="sxs-lookup"><span data-stu-id="499e9-345">If the previous try failed, the next try is after the **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="499e9-346">If it is 1:00 PM right now, we begin the first try.</span><span class="sxs-lookup"><span data-stu-id="499e9-346">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="499e9-347">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="499e9-347">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="499e9-348">For slices in the past, there is no delay.</span><span class="sxs-lookup"><span data-stu-id="499e9-348">For slices in the past, there is no delay.</span></span> <span data-ttu-id="499e9-349">The retry happens immediately.</span><span class="sxs-lookup"><span data-stu-id="499e9-349">The retry happens immediately.</span></span> |<span data-ttu-id="499e9-350">No</span><span class="sxs-lookup"><span data-stu-id="499e9-350">No</span></span> |<span data-ttu-id="499e9-351">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="499e9-351">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="499e9-352">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="499e9-352">retryTimeout</span></span> |<span data-ttu-id="499e9-353">The timeout for each retry attempt.</span><span class="sxs-lookup"><span data-stu-id="499e9-353">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="499e9-354">If this property is set to 10 minutes, the validation should be completed within 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="499e9-354">If this property is set to 10 minutes, the validation should be completed within 10 minutes.</span></span> <span data-ttu-id="499e9-355">If it takes longer than 10 minutes to perform the validation, the retry times out.</span><span class="sxs-lookup"><span data-stu-id="499e9-355">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="499e9-356">If all attempts for the validation time out, the slice is marked as **TimedOut**.</span><span class="sxs-lookup"><span data-stu-id="499e9-356">If all attempts for the validation time out, the slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="499e9-357">No</span><span class="sxs-lookup"><span data-stu-id="499e9-357">No</span></span> |<span data-ttu-id="499e9-358">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="499e9-358">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="499e9-359">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="499e9-359">maximumRetry</span></span> |<span data-ttu-id="499e9-360">The number of times to check for the availability of the external data.</span><span class="sxs-lookup"><span data-stu-id="499e9-360">The number of times to check for the availability of the external data.</span></span> <span data-ttu-id="499e9-361">The maximum allowed value is 10.</span><span class="sxs-lookup"><span data-stu-id="499e9-361">The maximum allowed value is 10.</span></span> |<span data-ttu-id="499e9-362">No</span><span class="sxs-lookup"><span data-stu-id="499e9-362">No</span></span> |<span data-ttu-id="499e9-363">3</span><span class="sxs-lookup"><span data-stu-id="499e9-363">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="499e9-364">Create datasets</span><span class="sxs-lookup"><span data-stu-id="499e9-364">Create datasets</span></span>
<span data-ttu-id="499e9-365">You can create datasets by using one of these tools or SDKs:</span><span class="sxs-lookup"><span data-stu-id="499e9-365">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="499e9-366">Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="499e9-366">Copy Wizard</span></span> 
- <span data-ttu-id="499e9-367">Azure portal</span><span class="sxs-lookup"><span data-stu-id="499e9-367">Azure portal</span></span>
- <span data-ttu-id="499e9-368">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="499e9-368">Visual Studio</span></span>
- <span data-ttu-id="499e9-369">PowerShell</span><span class="sxs-lookup"><span data-stu-id="499e9-369">PowerShell</span></span>
- <span data-ttu-id="499e9-370">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="499e9-370">Azure Resource Manager template</span></span>
- <span data-ttu-id="499e9-371">REST API</span><span class="sxs-lookup"><span data-stu-id="499e9-371">REST API</span></span>
- <span data-ttu-id="499e9-372">.NET API</span><span class="sxs-lookup"><span data-stu-id="499e9-372">.NET API</span></span>

<span data-ttu-id="499e9-373">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span><span class="sxs-lookup"><span data-stu-id="499e9-373">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="499e9-374">Build a pipeline with a data transformation activity</span><span class="sxs-lookup"><span data-stu-id="499e9-374">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="499e9-375">Build a pipeline with a data movement activity</span><span class="sxs-lookup"><span data-stu-id="499e9-375">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="499e9-376">After a pipeline is created and deployed, you can manage and monitor your pipelines by using the Azure portal blades, or the Monitoring and Management app.</span><span class="sxs-lookup"><span data-stu-id="499e9-376">After a pipeline is created and deployed, you can manage and monitor your pipelines by using the Azure portal blades, or the Monitoring and Management app.</span></span> <span data-ttu-id="499e9-377">See the following topics for step-by-step instructions:</span><span class="sxs-lookup"><span data-stu-id="499e9-377">See the following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="499e9-378">Monitor and manage pipelines by using Azure portal blades</span><span class="sxs-lookup"><span data-stu-id="499e9-378">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="499e9-379">Monitor and manage pipelines by using the Monitoring and Management app</span><span class="sxs-lookup"><span data-stu-id="499e9-379">Monitor and manage pipelines by using the Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="499e9-380">Scoped datasets</span><span class="sxs-lookup"><span data-stu-id="499e9-380">Scoped datasets</span></span>
<span data-ttu-id="499e9-381">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span><span class="sxs-lookup"><span data-stu-id="499e9-381">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span></span> <span data-ttu-id="499e9-382">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span><span class="sxs-lookup"><span data-stu-id="499e9-382">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="499e9-383">The following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) to be used within the pipeline.</span><span class="sxs-lookup"><span data-stu-id="499e9-383">The following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) to be used within the pipeline.</span></span>  

> [!IMPORTANT]
> Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set to **OneTime**). See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.
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

## <a name="next-steps"></a><span data-ttu-id="499e9-386">Next steps</span><span class="sxs-lookup"><span data-stu-id="499e9-386">Next steps</span></span>
- <span data-ttu-id="499e9-387">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="499e9-387">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="499e9-388">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="499e9-388">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
