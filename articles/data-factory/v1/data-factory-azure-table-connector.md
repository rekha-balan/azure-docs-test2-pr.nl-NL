---
title: Move data to/from Azure Table | Microsoft Docs
description: Learn how to move data to/from Azure Table Storage using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 3a24e919f1bbde6188e3655399f1ef843fbec23b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857711"
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="8d173-103">Move data to and from Azure Table using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8d173-103">Move data to and from Azure Table using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-azure-table-connector.md)
> * [Version 2 (current version)](../connector-azure-table-storage.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Azure Table Storage connector in V2](../connector-azure-table-storage.md).

<span data-ttu-id="8d173-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="8d173-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="8d173-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="8d173-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="8d173-110">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="8d173-110">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="8d173-111">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="8d173-111">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="8d173-112">Getting started</span><span class="sxs-lookup"><span data-stu-id="8d173-112">Getting started</span></span>
<span data-ttu-id="8d173-113">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="8d173-113">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="8d173-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="8d173-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8d173-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="8d173-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="8d173-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="8d173-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8d173-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="8d173-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8d173-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="8d173-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="8d173-119">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="8d173-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8d173-120">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="8d173-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8d173-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="8d173-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8d173-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="8d173-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8d173-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="8d173-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8d173-124">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="8d173-124">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="8d173-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span><span class="sxs-lookup"><span data-stu-id="8d173-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="8d173-126">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="8d173-126">Linked service properties</span></span>
<span data-ttu-id="8d173-127">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="8d173-127">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="8d173-128">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span><span class="sxs-lookup"><span data-stu-id="8d173-128">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="8d173-129">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8d173-129">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="8d173-130">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8d173-130">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="8d173-131">There are no other differences between these two linked services.</span><span class="sxs-lookup"><span data-stu-id="8d173-131">There are no other differences between these two linked services.</span></span> <span data-ttu-id="8d173-132">Choose the linked service that suits your needs.</span><span class="sxs-lookup"><span data-stu-id="8d173-132">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="8d173-133">The following sections provide more details on these two linked services.</span><span class="sxs-lookup"><span data-stu-id="8d173-133">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="8d173-134">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="8d173-134">Dataset properties</span></span>
<span data-ttu-id="8d173-135">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="8d173-135">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8d173-136">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="8d173-136">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8d173-137">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="8d173-137">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="8d173-138">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span><span class="sxs-lookup"><span data-stu-id="8d173-138">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="8d173-139">Property</span><span class="sxs-lookup"><span data-stu-id="8d173-139">Property</span></span> | <span data-ttu-id="8d173-140">Description</span><span class="sxs-lookup"><span data-stu-id="8d173-140">Description</span></span> | <span data-ttu-id="8d173-141">Required</span><span class="sxs-lookup"><span data-stu-id="8d173-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d173-142">tableName</span><span class="sxs-lookup"><span data-stu-id="8d173-142">tableName</span></span> |<span data-ttu-id="8d173-143">Name of the table in the Azure Table Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="8d173-143">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="8d173-144">Yes.</span><span class="sxs-lookup"><span data-stu-id="8d173-144">Yes.</span></span> <span data-ttu-id="8d173-145">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="8d173-145">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="8d173-146">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="8d173-146">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="8d173-147">Schema by Data Factory</span><span class="sxs-lookup"><span data-stu-id="8d173-147">Schema by Data Factory</span></span>
<span data-ttu-id="8d173-148">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="8d173-148">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="8d173-149">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span><span class="sxs-lookup"><span data-stu-id="8d173-149">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="8d173-150">In this case, if a row does not contain a value for a column, a null value is provided for it.</span><span class="sxs-lookup"><span data-stu-id="8d173-150">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="8d173-151">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span><span class="sxs-lookup"><span data-stu-id="8d173-151">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="8d173-152">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span><span class="sxs-lookup"><span data-stu-id="8d173-152">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="8d173-153">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span><span class="sxs-lookup"><span data-stu-id="8d173-153">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="8d173-154">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="8d173-154">Copy activity properties</span></span>
<span data-ttu-id="8d173-155">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="8d173-155">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8d173-156">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="8d173-156">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="8d173-157">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="8d173-157">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="8d173-158">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="8d173-158">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="8d173-159">**AzureTableSource** supports the following properties in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="8d173-159">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="8d173-160">Property</span><span class="sxs-lookup"><span data-stu-id="8d173-160">Property</span></span> | <span data-ttu-id="8d173-161">Description</span><span class="sxs-lookup"><span data-stu-id="8d173-161">Description</span></span> | <span data-ttu-id="8d173-162">Allowed values</span><span class="sxs-lookup"><span data-stu-id="8d173-162">Allowed values</span></span> | <span data-ttu-id="8d173-163">Required</span><span class="sxs-lookup"><span data-stu-id="8d173-163">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8d173-164">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="8d173-164">azureTableSourceQuery</span></span> |<span data-ttu-id="8d173-165">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="8d173-165">Use the custom query to read data.</span></span> |<span data-ttu-id="8d173-166">Azure table query string.</span><span class="sxs-lookup"><span data-stu-id="8d173-166">Azure table query string.</span></span> <span data-ttu-id="8d173-167">See examples in the next section.</span><span class="sxs-lookup"><span data-stu-id="8d173-167">See examples in the next section.</span></span> |<span data-ttu-id="8d173-168">No.</span><span class="sxs-lookup"><span data-stu-id="8d173-168">No.</span></span> <span data-ttu-id="8d173-169">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="8d173-169">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="8d173-170">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="8d173-170">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="8d173-171">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="8d173-171">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="8d173-172">Indicate whether swallow the exception of table not exist.</span><span class="sxs-lookup"><span data-stu-id="8d173-172">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="8d173-173">TRUE</span><span class="sxs-lookup"><span data-stu-id="8d173-173">TRUE</span></span><br/><span data-ttu-id="8d173-174">FALSE</span><span class="sxs-lookup"><span data-stu-id="8d173-174">FALSE</span></span> |<span data-ttu-id="8d173-175">No</span><span class="sxs-lookup"><span data-stu-id="8d173-175">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="8d173-176">azureTableSourceQuery examples</span><span class="sxs-lookup"><span data-stu-id="8d173-176">azureTableSourceQuery examples</span></span>
<span data-ttu-id="8d173-177">If Azure Table column is of string type:</span><span class="sxs-lookup"><span data-stu-id="8d173-177">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="8d173-178">If Azure Table column is of datetime type:</span><span class="sxs-lookup"><span data-stu-id="8d173-178">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="8d173-179">**AzureTableSink** supports the following properties in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="8d173-179">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="8d173-180">Property</span><span class="sxs-lookup"><span data-stu-id="8d173-180">Property</span></span> | <span data-ttu-id="8d173-181">Description</span><span class="sxs-lookup"><span data-stu-id="8d173-181">Description</span></span> | <span data-ttu-id="8d173-182">Allowed values</span><span class="sxs-lookup"><span data-stu-id="8d173-182">Allowed values</span></span> | <span data-ttu-id="8d173-183">Required</span><span class="sxs-lookup"><span data-stu-id="8d173-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8d173-184">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="8d173-184">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="8d173-185">Default partition key value that can be used by the sink.</span><span class="sxs-lookup"><span data-stu-id="8d173-185">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="8d173-186">A string value.</span><span class="sxs-lookup"><span data-stu-id="8d173-186">A string value.</span></span> |<span data-ttu-id="8d173-187">No</span><span class="sxs-lookup"><span data-stu-id="8d173-187">No</span></span> |
| <span data-ttu-id="8d173-188">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="8d173-188">azureTablePartitionKeyName</span></span> |<span data-ttu-id="8d173-189">Specify name of the column whose values are used as partition keys.</span><span class="sxs-lookup"><span data-stu-id="8d173-189">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="8d173-190">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span><span class="sxs-lookup"><span data-stu-id="8d173-190">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="8d173-191">A column name.</span><span class="sxs-lookup"><span data-stu-id="8d173-191">A column name.</span></span> |<span data-ttu-id="8d173-192">No</span><span class="sxs-lookup"><span data-stu-id="8d173-192">No</span></span> |
| <span data-ttu-id="8d173-193">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="8d173-193">azureTableRowKeyName</span></span> |<span data-ttu-id="8d173-194">Specify name of the column whose column values are used as row key.</span><span class="sxs-lookup"><span data-stu-id="8d173-194">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="8d173-195">If not specified, use a GUID for each row.</span><span class="sxs-lookup"><span data-stu-id="8d173-195">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="8d173-196">A column name.</span><span class="sxs-lookup"><span data-stu-id="8d173-196">A column name.</span></span> |<span data-ttu-id="8d173-197">No</span><span class="sxs-lookup"><span data-stu-id="8d173-197">No</span></span> |
| <span data-ttu-id="8d173-198">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="8d173-198">azureTableInsertType</span></span> |<span data-ttu-id="8d173-199">The mode to insert data into Azure table.</span><span class="sxs-lookup"><span data-stu-id="8d173-199">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="8d173-200">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span><span class="sxs-lookup"><span data-stu-id="8d173-200">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="8d173-201">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span><span class="sxs-lookup"><span data-stu-id="8d173-201">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="8d173-202">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span><span class="sxs-lookup"><span data-stu-id="8d173-202">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="8d173-203">merge (default)</span><span class="sxs-lookup"><span data-stu-id="8d173-203">merge (default)</span></span><br/><span data-ttu-id="8d173-204">replace</span><span class="sxs-lookup"><span data-stu-id="8d173-204">replace</span></span> |<span data-ttu-id="8d173-205">No</span><span class="sxs-lookup"><span data-stu-id="8d173-205">No</span></span> |
| <span data-ttu-id="8d173-206">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8d173-206">writeBatchSize</span></span> |<span data-ttu-id="8d173-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span><span class="sxs-lookup"><span data-stu-id="8d173-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="8d173-208">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="8d173-208">Integer (number of rows)</span></span> |<span data-ttu-id="8d173-209">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="8d173-209">No (default: 10000)</span></span> |
| <span data-ttu-id="8d173-210">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8d173-210">writeBatchTimeout</span></span> |<span data-ttu-id="8d173-211">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span><span class="sxs-lookup"><span data-stu-id="8d173-211">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="8d173-212">timespan</span><span class="sxs-lookup"><span data-stu-id="8d173-212">timespan</span></span><br/><br/><span data-ttu-id="8d173-213">Example: “00:20:00” (20 minutes)</span><span class="sxs-lookup"><span data-stu-id="8d173-213">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="8d173-214">No (Default to storage client default timeout value 90 sec)</span><span class="sxs-lookup"><span data-stu-id="8d173-214">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="8d173-215">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="8d173-215">azureTablePartitionKeyName</span></span>
<span data-ttu-id="8d173-216">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="8d173-216">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="8d173-217">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="8d173-217">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="8d173-218">The DivisionID is specified as the partition key.</span><span class="sxs-lookup"><span data-stu-id="8d173-218">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="8d173-219">JSON examples</span><span class="sxs-lookup"><span data-stu-id="8d173-219">JSON examples</span></span>
<span data-ttu-id="8d173-220">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8d173-220">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8d173-221">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span><span class="sxs-lookup"><span data-stu-id="8d173-221">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="8d173-222">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span><span class="sxs-lookup"><span data-stu-id="8d173-222">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="8d173-223">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8d173-223">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="8d173-224">Example: Copy data from Azure Table to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="8d173-224">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="8d173-225">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="8d173-225">The following sample shows:</span></span>

1. <span data-ttu-id="8d173-226">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span><span class="sxs-lookup"><span data-stu-id="8d173-226">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="8d173-227">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8d173-227">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="8d173-228">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8d173-228">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8d173-229">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8d173-229">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8d173-230">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="8d173-230">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="8d173-231">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="8d173-231">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8d173-232">**Azure storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="8d173-232">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="8d173-233">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="8d173-233">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="8d173-234">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span><span class="sxs-lookup"><span data-stu-id="8d173-234">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="8d173-235">See [Linked Services](#linked-service-properties) section for details.</span><span class="sxs-lookup"><span data-stu-id="8d173-235">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="8d173-236">**Azure Table input dataset:**</span><span class="sxs-lookup"><span data-stu-id="8d173-236">**Azure Table input dataset:**</span></span>

<span data-ttu-id="8d173-237">The sample assumes you have created a table “MyTable” in Azure Table.</span><span class="sxs-lookup"><span data-stu-id="8d173-237">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="8d173-238">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="8d173-238">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="8d173-239">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="8d173-239">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8d173-240">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="8d173-240">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8d173-241">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="8d173-241">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="8d173-242">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="8d173-242">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="8d173-243">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="8d173-243">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="8d173-244">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="8d173-244">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="8d173-245">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8d173-245">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="8d173-246">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span><span class="sxs-lookup"><span data-stu-id="8d173-246">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="8d173-247">Example: Copy data from Azure Blob to Azure Table</span><span class="sxs-lookup"><span data-stu-id="8d173-247">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="8d173-248">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="8d173-248">The following sample shows:</span></span>

1. <span data-ttu-id="8d173-249">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span><span class="sxs-lookup"><span data-stu-id="8d173-249">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="8d173-250">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8d173-250">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="8d173-251">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8d173-251">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="8d173-252">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8d173-252">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="8d173-253">The sample copies time-series data from an Azure blob to an Azure table hourly.</span><span class="sxs-lookup"><span data-stu-id="8d173-253">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="8d173-254">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="8d173-254">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8d173-255">**Azure storage (for both Azure Table & Blob) linked service:**</span><span class="sxs-lookup"><span data-stu-id="8d173-255">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="8d173-256">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="8d173-256">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="8d173-257">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span><span class="sxs-lookup"><span data-stu-id="8d173-257">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="8d173-258">See [Linked Services](#linked-service-properties) section for details.</span><span class="sxs-lookup"><span data-stu-id="8d173-258">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="8d173-259">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="8d173-259">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="8d173-260">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="8d173-260">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8d173-261">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="8d173-261">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="8d173-262">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="8d173-262">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="8d173-263">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="8d173-263">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="8d173-264">**Azure Table output dataset:**</span><span class="sxs-lookup"><span data-stu-id="8d173-264">**Azure Table output dataset:**</span></span>

<span data-ttu-id="8d173-265">The sample copies data to a table named “MyTable” in Azure Table.</span><span class="sxs-lookup"><span data-stu-id="8d173-265">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="8d173-266">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="8d173-266">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="8d173-267">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="8d173-267">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="8d173-268">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="8d173-268">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="8d173-269">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="8d173-269">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="8d173-270">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="8d173-270">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="8d173-271">Type Mapping for Azure Table</span><span class="sxs-lookup"><span data-stu-id="8d173-271">Type Mapping for Azure Table</span></span>
<span data-ttu-id="8d173-272">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span><span class="sxs-lookup"><span data-stu-id="8d173-272">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="8d173-273">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="8d173-273">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="8d173-274">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="8d173-274">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="8d173-275">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="8d173-275">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="8d173-276">OData Data Type</span><span class="sxs-lookup"><span data-stu-id="8d173-276">OData Data Type</span></span> | <span data-ttu-id="8d173-277">.NET Type</span><span class="sxs-lookup"><span data-stu-id="8d173-277">.NET Type</span></span> | <span data-ttu-id="8d173-278">Details</span><span class="sxs-lookup"><span data-stu-id="8d173-278">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d173-279">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="8d173-279">Edm.Binary</span></span> |<span data-ttu-id="8d173-280">byte[]</span><span class="sxs-lookup"><span data-stu-id="8d173-280">byte[]</span></span> |<span data-ttu-id="8d173-281">An array of bytes up to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="8d173-281">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="8d173-282">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="8d173-282">Edm.Boolean</span></span> |<span data-ttu-id="8d173-283">bool</span><span class="sxs-lookup"><span data-stu-id="8d173-283">bool</span></span> |<span data-ttu-id="8d173-284">A Boolean value.</span><span class="sxs-lookup"><span data-stu-id="8d173-284">A Boolean value.</span></span> |
| <span data-ttu-id="8d173-285">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="8d173-285">Edm.DateTime</span></span> |<span data-ttu-id="8d173-286">DateTime</span><span class="sxs-lookup"><span data-stu-id="8d173-286">DateTime</span></span> |<span data-ttu-id="8d173-287">A 64-bit value expressed as Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="8d173-287">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="8d173-288">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span><span class="sxs-lookup"><span data-stu-id="8d173-288">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="8d173-289">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="8d173-289">(C.E.), UTC.</span></span> <span data-ttu-id="8d173-290">The range ends at December 31, 9999.</span><span class="sxs-lookup"><span data-stu-id="8d173-290">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="8d173-291">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="8d173-291">Edm.Double</span></span> |<span data-ttu-id="8d173-292">double</span><span class="sxs-lookup"><span data-stu-id="8d173-292">double</span></span> |<span data-ttu-id="8d173-293">A 64-bit floating point value.</span><span class="sxs-lookup"><span data-stu-id="8d173-293">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="8d173-294">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="8d173-294">Edm.Guid</span></span> |<span data-ttu-id="8d173-295">Guid</span><span class="sxs-lookup"><span data-stu-id="8d173-295">Guid</span></span> |<span data-ttu-id="8d173-296">A 128-bit globally unique identifier.</span><span class="sxs-lookup"><span data-stu-id="8d173-296">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="8d173-297">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="8d173-297">Edm.Int32</span></span> |<span data-ttu-id="8d173-298">Int32</span><span class="sxs-lookup"><span data-stu-id="8d173-298">Int32</span></span> |<span data-ttu-id="8d173-299">A 32-bit integer.</span><span class="sxs-lookup"><span data-stu-id="8d173-299">A 32-bit integer.</span></span> |
| <span data-ttu-id="8d173-300">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="8d173-300">Edm.Int64</span></span> |<span data-ttu-id="8d173-301">Int64</span><span class="sxs-lookup"><span data-stu-id="8d173-301">Int64</span></span> |<span data-ttu-id="8d173-302">A 64-bit integer.</span><span class="sxs-lookup"><span data-stu-id="8d173-302">A 64-bit integer.</span></span> |
| <span data-ttu-id="8d173-303">Edm.String</span><span class="sxs-lookup"><span data-stu-id="8d173-303">Edm.String</span></span> |<span data-ttu-id="8d173-304">String</span><span class="sxs-lookup"><span data-stu-id="8d173-304">String</span></span> |<span data-ttu-id="8d173-305">A UTF-16-encoded value.</span><span class="sxs-lookup"><span data-stu-id="8d173-305">A UTF-16-encoded value.</span></span> <span data-ttu-id="8d173-306">String values may be up to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="8d173-306">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="8d173-307">Type Conversion Sample</span><span class="sxs-lookup"><span data-stu-id="8d173-307">Type Conversion Sample</span></span>
<span data-ttu-id="8d173-308">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span><span class="sxs-lookup"><span data-stu-id="8d173-308">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="8d173-309">Suppose the Blob dataset is in CSV format and contains three columns.</span><span class="sxs-lookup"><span data-stu-id="8d173-309">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="8d173-310">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span><span class="sxs-lookup"><span data-stu-id="8d173-310">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="8d173-311">Define the Blob Source dataset as follows along with type definitions for the columns.</span><span class="sxs-lookup"><span data-stu-id="8d173-311">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

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
<span data-ttu-id="8d173-312">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span><span class="sxs-lookup"><span data-stu-id="8d173-312">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="8d173-313">**Azure Table schema:**</span><span class="sxs-lookup"><span data-stu-id="8d173-313">**Azure Table schema:**</span></span>

| <span data-ttu-id="8d173-314">Column name</span><span class="sxs-lookup"><span data-stu-id="8d173-314">Column name</span></span> | <span data-ttu-id="8d173-315">Type</span><span class="sxs-lookup"><span data-stu-id="8d173-315">Type</span></span> |
| --- | --- |
| <span data-ttu-id="8d173-316">userid</span><span class="sxs-lookup"><span data-stu-id="8d173-316">userid</span></span> |<span data-ttu-id="8d173-317">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="8d173-317">Edm.Int64</span></span> |
| <span data-ttu-id="8d173-318">name</span><span class="sxs-lookup"><span data-stu-id="8d173-318">name</span></span> |<span data-ttu-id="8d173-319">Edm.String</span><span class="sxs-lookup"><span data-stu-id="8d173-319">Edm.String</span></span> |
| <span data-ttu-id="8d173-320">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="8d173-320">lastlogindate</span></span> |<span data-ttu-id="8d173-321">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="8d173-321">Edm.DateTime</span></span> |

<span data-ttu-id="8d173-322">Next, define the Azure Table dataset as follows.</span><span class="sxs-lookup"><span data-stu-id="8d173-322">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="8d173-323">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span><span class="sxs-lookup"><span data-stu-id="8d173-323">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

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

<span data-ttu-id="8d173-324">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span><span class="sxs-lookup"><span data-stu-id="8d173-324">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a><span data-ttu-id="8d173-326">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="8d173-326">Performance and Tuning</span></span>
<span data-ttu-id="8d173-327">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="8d173-327">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
