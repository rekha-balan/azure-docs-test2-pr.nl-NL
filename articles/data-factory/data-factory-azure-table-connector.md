---
title: Move data to/from Azure Table | Microsoft Docs
description: Learn how to move data to/from Azure Table Storage using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jingwang
ms.openlocfilehash: d688b5c6f918542b73d95c795f5dbb82070b17c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564116"
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="26190-103">Move data to and from Azure Table using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="26190-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="26190-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="26190-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="26190-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="26190-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="26190-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="26190-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="26190-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="26190-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="26190-108">Getting started</span><span class="sxs-lookup"><span data-stu-id="26190-108">Getting started</span></span>
<span data-ttu-id="26190-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="26190-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="26190-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="26190-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="26190-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="26190-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="26190-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="26190-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="26190-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="26190-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="26190-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="26190-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="26190-115">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="26190-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="26190-116">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="26190-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="26190-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="26190-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="26190-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="26190-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="26190-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="26190-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="26190-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="26190-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="26190-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span><span class="sxs-lookup"><span data-stu-id="26190-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="26190-122">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="26190-122">Linked service properties</span></span>
<span data-ttu-id="26190-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="26190-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="26190-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span><span class="sxs-lookup"><span data-stu-id="26190-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="26190-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="26190-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="26190-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="26190-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="26190-127">There are no other differences between these two linked services.</span><span class="sxs-lookup"><span data-stu-id="26190-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="26190-128">Choose the linked service that suits your needs.</span><span class="sxs-lookup"><span data-stu-id="26190-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="26190-129">The following sections provide more details on these two linked services.</span><span class="sxs-lookup"><span data-stu-id="26190-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="26190-130">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="26190-130">Dataset properties</span></span>
<span data-ttu-id="26190-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="26190-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="26190-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="26190-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="26190-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="26190-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="26190-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span><span class="sxs-lookup"><span data-stu-id="26190-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="26190-135">Property</span><span class="sxs-lookup"><span data-stu-id="26190-135">Property</span></span> | <span data-ttu-id="26190-136">Description</span><span class="sxs-lookup"><span data-stu-id="26190-136">Description</span></span> | <span data-ttu-id="26190-137">Required</span><span class="sxs-lookup"><span data-stu-id="26190-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26190-138">tableName</span><span class="sxs-lookup"><span data-stu-id="26190-138">tableName</span></span> |<span data-ttu-id="26190-139">Name of the table in the Azure Table Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="26190-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="26190-140">Yes.</span><span class="sxs-lookup"><span data-stu-id="26190-140">Yes.</span></span> <span data-ttu-id="26190-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="26190-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="26190-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="26190-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="26190-143">Schema by Data Factory</span><span class="sxs-lookup"><span data-stu-id="26190-143">Schema by Data Factory</span></span>
<span data-ttu-id="26190-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="26190-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="26190-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span><span class="sxs-lookup"><span data-stu-id="26190-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="26190-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span><span class="sxs-lookup"><span data-stu-id="26190-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="26190-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span><span class="sxs-lookup"><span data-stu-id="26190-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="26190-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span><span class="sxs-lookup"><span data-stu-id="26190-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="26190-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span><span class="sxs-lookup"><span data-stu-id="26190-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="26190-150">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="26190-150">Copy activity properties</span></span>
<span data-ttu-id="26190-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="26190-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="26190-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="26190-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="26190-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="26190-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="26190-154">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="26190-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="26190-155">**AzureTableSource** supports the following properties in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="26190-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="26190-156">Property</span><span class="sxs-lookup"><span data-stu-id="26190-156">Property</span></span> | <span data-ttu-id="26190-157">Description</span><span class="sxs-lookup"><span data-stu-id="26190-157">Description</span></span> | <span data-ttu-id="26190-158">Allowed values</span><span class="sxs-lookup"><span data-stu-id="26190-158">Allowed values</span></span> | <span data-ttu-id="26190-159">Required</span><span class="sxs-lookup"><span data-stu-id="26190-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26190-160">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="26190-160">azureTableSourceQuery</span></span> |<span data-ttu-id="26190-161">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="26190-161">Use the custom query to read data.</span></span> |<span data-ttu-id="26190-162">Azure table query string.</span><span class="sxs-lookup"><span data-stu-id="26190-162">Azure table query string.</span></span> <span data-ttu-id="26190-163">See examples in the next section.</span><span class="sxs-lookup"><span data-stu-id="26190-163">See examples in the next section.</span></span> |<span data-ttu-id="26190-164">No.</span><span class="sxs-lookup"><span data-stu-id="26190-164">No.</span></span> <span data-ttu-id="26190-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="26190-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="26190-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="26190-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="26190-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="26190-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="26190-168">Indicate whether swallow the exception of table not exist.</span><span class="sxs-lookup"><span data-stu-id="26190-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="26190-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="26190-169">TRUE</span></span><br/><span data-ttu-id="26190-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="26190-170">FALSE</span></span> |<span data-ttu-id="26190-171">No</span><span class="sxs-lookup"><span data-stu-id="26190-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="26190-172">azureTableSourceQuery examples</span><span class="sxs-lookup"><span data-stu-id="26190-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="26190-173">If Azure Table column is of string type:</span><span class="sxs-lookup"><span data-stu-id="26190-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="26190-174">If Azure Table column is of datetime type:</span><span class="sxs-lookup"><span data-stu-id="26190-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="26190-175">**AzureTableSink** supports the following properties in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="26190-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="26190-176">Property</span><span class="sxs-lookup"><span data-stu-id="26190-176">Property</span></span> | <span data-ttu-id="26190-177">Description</span><span class="sxs-lookup"><span data-stu-id="26190-177">Description</span></span> | <span data-ttu-id="26190-178">Allowed values</span><span class="sxs-lookup"><span data-stu-id="26190-178">Allowed values</span></span> | <span data-ttu-id="26190-179">Required</span><span class="sxs-lookup"><span data-stu-id="26190-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26190-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="26190-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="26190-181">Default partition key value that can be used by the sink.</span><span class="sxs-lookup"><span data-stu-id="26190-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="26190-182">A string value.</span><span class="sxs-lookup"><span data-stu-id="26190-182">A string value.</span></span> |<span data-ttu-id="26190-183">No</span><span class="sxs-lookup"><span data-stu-id="26190-183">No</span></span> |
| <span data-ttu-id="26190-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="26190-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="26190-185">Specify name of the column whose values are used as partition keys.</span><span class="sxs-lookup"><span data-stu-id="26190-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="26190-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span><span class="sxs-lookup"><span data-stu-id="26190-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="26190-187">A column name.</span><span class="sxs-lookup"><span data-stu-id="26190-187">A column name.</span></span> |<span data-ttu-id="26190-188">No</span><span class="sxs-lookup"><span data-stu-id="26190-188">No</span></span> |
| <span data-ttu-id="26190-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="26190-189">azureTableRowKeyName</span></span> |<span data-ttu-id="26190-190">Specify name of the column whose column values are used as row key.</span><span class="sxs-lookup"><span data-stu-id="26190-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="26190-191">If not specified, use a GUID for each row.</span><span class="sxs-lookup"><span data-stu-id="26190-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="26190-192">A column name.</span><span class="sxs-lookup"><span data-stu-id="26190-192">A column name.</span></span> |<span data-ttu-id="26190-193">No</span><span class="sxs-lookup"><span data-stu-id="26190-193">No</span></span> |
| <span data-ttu-id="26190-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="26190-194">azureTableInsertType</span></span> |<span data-ttu-id="26190-195">The mode to insert data into Azure table.</span><span class="sxs-lookup"><span data-stu-id="26190-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="26190-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span><span class="sxs-lookup"><span data-stu-id="26190-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="26190-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span><span class="sxs-lookup"><span data-stu-id="26190-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="26190-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span><span class="sxs-lookup"><span data-stu-id="26190-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="26190-199">merge (default)</span><span class="sxs-lookup"><span data-stu-id="26190-199">merge (default)</span></span><br/><span data-ttu-id="26190-200">replace</span><span class="sxs-lookup"><span data-stu-id="26190-200">replace</span></span> |<span data-ttu-id="26190-201">No</span><span class="sxs-lookup"><span data-stu-id="26190-201">No</span></span> |
| <span data-ttu-id="26190-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="26190-202">writeBatchSize</span></span> |<span data-ttu-id="26190-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span><span class="sxs-lookup"><span data-stu-id="26190-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="26190-204">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="26190-204">Integer (number of rows)</span></span> |<span data-ttu-id="26190-205">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="26190-205">No (default: 10000)</span></span> |
| <span data-ttu-id="26190-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="26190-206">writeBatchTimeout</span></span> |<span data-ttu-id="26190-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span><span class="sxs-lookup"><span data-stu-id="26190-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="26190-208">timespan</span><span class="sxs-lookup"><span data-stu-id="26190-208">timespan</span></span><br/><br/><span data-ttu-id="26190-209">Example: “00:20:00” (20 minutes)</span><span class="sxs-lookup"><span data-stu-id="26190-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="26190-210">No (Default to storage client default timeout value 90 sec)</span><span class="sxs-lookup"><span data-stu-id="26190-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="26190-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="26190-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="26190-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="26190-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="26190-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="26190-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="26190-214">The DivisionID is specified as the partition key.</span><span class="sxs-lookup"><span data-stu-id="26190-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="26190-215">JSON examples</span><span class="sxs-lookup"><span data-stu-id="26190-215">JSON examples</span></span>
<span data-ttu-id="26190-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="26190-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="26190-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span><span class="sxs-lookup"><span data-stu-id="26190-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="26190-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span><span class="sxs-lookup"><span data-stu-id="26190-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="26190-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="26190-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="26190-220">Example: Copy data from Azure Table to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="26190-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="26190-221">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="26190-221">The following sample shows:</span></span>

1. <span data-ttu-id="26190-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span><span class="sxs-lookup"><span data-stu-id="26190-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="26190-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26190-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="26190-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26190-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="26190-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="26190-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="26190-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="26190-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="26190-227">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="26190-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="26190-228">**Azure storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="26190-228">**Azure storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="26190-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="26190-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="26190-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span><span class="sxs-lookup"><span data-stu-id="26190-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="26190-231">See [Linked Services](#linked-service-properties) section for details.</span><span class="sxs-lookup"><span data-stu-id="26190-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="26190-232">**Azure Table input dataset:**</span><span class="sxs-lookup"><span data-stu-id="26190-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="26190-233">The sample assumes you have created a table “MyTable” in Azure Table.</span><span class="sxs-lookup"><span data-stu-id="26190-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="26190-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="26190-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="26190-235">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="26190-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="26190-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="26190-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="26190-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="26190-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="26190-238">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="26190-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="26190-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="26190-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="26190-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="26190-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="26190-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="26190-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="26190-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span><span class="sxs-lookup"><span data-stu-id="26190-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },                
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="26190-243">Example: Copy data from Azure Blob to Azure Table</span><span class="sxs-lookup"><span data-stu-id="26190-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="26190-244">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="26190-244">The following sample shows:</span></span>

1. <span data-ttu-id="26190-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span><span class="sxs-lookup"><span data-stu-id="26190-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="26190-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26190-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="26190-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26190-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="26190-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="26190-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="26190-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span><span class="sxs-lookup"><span data-stu-id="26190-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="26190-250">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="26190-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="26190-251">**Azure storage (for both Azure Table & Blob) linked service:**</span><span class="sxs-lookup"><span data-stu-id="26190-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="26190-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="26190-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="26190-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span><span class="sxs-lookup"><span data-stu-id="26190-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="26190-254">See [Linked Services](#linked-service-properties) section for details.</span><span class="sxs-lookup"><span data-stu-id="26190-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="26190-255">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="26190-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="26190-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="26190-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="26190-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="26190-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="26190-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="26190-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="26190-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="26190-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="26190-260">**Azure Table output dataset:**</span><span class="sxs-lookup"><span data-stu-id="26190-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="26190-261">The sample copies data to a table named “MyTable” in Azure Table.</span><span class="sxs-lookup"><span data-stu-id="26190-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="26190-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="26190-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="26190-263">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="26190-263">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="26190-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="26190-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="26190-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="26190-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="26190-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="26190-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
          }
        },
        "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },                        
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
### <a name="type-mapping-for-azure-table"></a><span data-ttu-id="26190-267">Type Mapping for Azure Table</span><span class="sxs-lookup"><span data-stu-id="26190-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="26190-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span><span class="sxs-lookup"><span data-stu-id="26190-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="26190-269">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="26190-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="26190-270">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="26190-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="26190-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="26190-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="26190-272">OData Data Type</span><span class="sxs-lookup"><span data-stu-id="26190-272">OData Data Type</span></span> | <span data-ttu-id="26190-273">.NET Type</span><span class="sxs-lookup"><span data-stu-id="26190-273">.NET Type</span></span> | <span data-ttu-id="26190-274">Details</span><span class="sxs-lookup"><span data-stu-id="26190-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26190-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="26190-275">Edm.Binary</span></span> |<span data-ttu-id="26190-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="26190-276">byte[]</span></span> |<span data-ttu-id="26190-277">An array of bytes up to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="26190-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="26190-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="26190-278">Edm.Boolean</span></span> |<span data-ttu-id="26190-279">bool</span><span class="sxs-lookup"><span data-stu-id="26190-279">bool</span></span> |<span data-ttu-id="26190-280">A Boolean value.</span><span class="sxs-lookup"><span data-stu-id="26190-280">A Boolean value.</span></span> |
| <span data-ttu-id="26190-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="26190-281">Edm.DateTime</span></span> |<span data-ttu-id="26190-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="26190-282">DateTime</span></span> |<span data-ttu-id="26190-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="26190-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="26190-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span><span class="sxs-lookup"><span data-stu-id="26190-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="26190-285">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="26190-285">(C.E.), UTC.</span></span> <span data-ttu-id="26190-286">The range ends at December 31, 9999.</span><span class="sxs-lookup"><span data-stu-id="26190-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="26190-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="26190-287">Edm.Double</span></span> |<span data-ttu-id="26190-288">double</span><span class="sxs-lookup"><span data-stu-id="26190-288">double</span></span> |<span data-ttu-id="26190-289">A 64-bit floating point value.</span><span class="sxs-lookup"><span data-stu-id="26190-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="26190-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="26190-290">Edm.Guid</span></span> |<span data-ttu-id="26190-291">Guid</span><span class="sxs-lookup"><span data-stu-id="26190-291">Guid</span></span> |<span data-ttu-id="26190-292">A 128-bit globally unique identifier.</span><span class="sxs-lookup"><span data-stu-id="26190-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="26190-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="26190-293">Edm.Int32</span></span> |<span data-ttu-id="26190-294">Int32 or int</span><span class="sxs-lookup"><span data-stu-id="26190-294">Int32 or int</span></span> |<span data-ttu-id="26190-295">A 32-bit integer.</span><span class="sxs-lookup"><span data-stu-id="26190-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="26190-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="26190-296">Edm.Int64</span></span> |<span data-ttu-id="26190-297">Int64 or long</span><span class="sxs-lookup"><span data-stu-id="26190-297">Int64 or long</span></span> |<span data-ttu-id="26190-298">A 64-bit integer.</span><span class="sxs-lookup"><span data-stu-id="26190-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="26190-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="26190-299">Edm.String</span></span> |<span data-ttu-id="26190-300">String</span><span class="sxs-lookup"><span data-stu-id="26190-300">String</span></span> |<span data-ttu-id="26190-301">A UTF-16-encoded value.</span><span class="sxs-lookup"><span data-stu-id="26190-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="26190-302">String values may be up to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="26190-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="26190-303">Type Conversion Sample</span><span class="sxs-lookup"><span data-stu-id="26190-303">Type Conversion Sample</span></span>
<span data-ttu-id="26190-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span><span class="sxs-lookup"><span data-stu-id="26190-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="26190-305">Suppose the Blob dataset is in CSV format and contains three columns.</span><span class="sxs-lookup"><span data-stu-id="26190-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="26190-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span><span class="sxs-lookup"><span data-stu-id="26190-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="26190-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span><span class="sxs-lookup"><span data-stu-id="26190-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="26190-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span><span class="sxs-lookup"><span data-stu-id="26190-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="26190-309">**Azure Table schema:**</span><span class="sxs-lookup"><span data-stu-id="26190-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="26190-310">Column name</span><span class="sxs-lookup"><span data-stu-id="26190-310">Column name</span></span> | <span data-ttu-id="26190-311">Type</span><span class="sxs-lookup"><span data-stu-id="26190-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="26190-312">userid</span><span class="sxs-lookup"><span data-stu-id="26190-312">userid</span></span> |<span data-ttu-id="26190-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="26190-313">Edm.Int64</span></span> |
| <span data-ttu-id="26190-314">name</span><span class="sxs-lookup"><span data-stu-id="26190-314">name</span></span> |<span data-ttu-id="26190-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="26190-315">Edm.String</span></span> |
| <span data-ttu-id="26190-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="26190-316">lastlogindate</span></span> |<span data-ttu-id="26190-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="26190-317">Edm.DateTime</span></span> |

<span data-ttu-id="26190-318">Next, define the Azure Table dataset as follows.</span><span class="sxs-lookup"><span data-stu-id="26190-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="26190-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span><span class="sxs-lookup"><span data-stu-id="26190-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="26190-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span><span class="sxs-lookup"><span data-stu-id="26190-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="26190-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="26190-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="26190-322">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="26190-322">Performance and Tuning</span></span>
<span data-ttu-id="26190-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="26190-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
