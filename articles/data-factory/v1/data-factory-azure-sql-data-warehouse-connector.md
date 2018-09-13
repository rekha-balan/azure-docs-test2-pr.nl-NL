---
title: Copy data to/from Azure SQL Data Warehouse | Microsoft Docs
description: Learn how to copy data to/from Azure SQL Data Warehouse using Azure Data Factory
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 678913796edafe86e19d8907e3a2e29ec15ffa90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857275"
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="eed7e-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="eed7e-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-azure-sql-data-warehouse-connector.md)
> * [Version 2 (current version)](../connector-azure-sql-data-warehouse.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Azure SQL Data Warehouse connector in V2](../connector-azure-sql-data-warehouse.md).

<span data-ttu-id="eed7e-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eed7e-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="eed7e-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="eed7e-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse. The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details. For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).

## <a name="supported-scenarios"></a><span data-ttu-id="eed7e-113">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="eed7e-113">Supported scenarios</span></span>
<span data-ttu-id="eed7e-114">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span><span class="sxs-lookup"><span data-stu-id="eed7e-114">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="eed7e-115">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="eed7e-115">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../../includes/data-factory-supported-sources.md)]

> [!TIP]
> When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store. See [Auto table creation](#auto-table-creation) for details.

## <a name="supported-authentication-type"></a><span data-ttu-id="eed7e-118">Supported authentication type</span><span class="sxs-lookup"><span data-stu-id="eed7e-118">Supported authentication type</span></span>
<span data-ttu-id="eed7e-119">Azure SQL Data Warehouse connector support basic authentication.</span><span class="sxs-lookup"><span data-stu-id="eed7e-119">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="eed7e-120">Getting started</span><span class="sxs-lookup"><span data-stu-id="eed7e-120">Getting started</span></span>
<span data-ttu-id="eed7e-121">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="eed7e-121">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="eed7e-122">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="eed7e-122">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="eed7e-123">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="eed7e-123">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="eed7e-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="eed7e-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="eed7e-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="eed7e-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="eed7e-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="eed7e-127">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-127">Create a **data factory**.</span></span> <span data-ttu-id="eed7e-128">A data factory may contain one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="eed7e-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="eed7e-129">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="eed7e-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="eed7e-130">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span><span class="sxs-lookup"><span data-stu-id="eed7e-130">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="eed7e-131">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="eed7e-131">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="eed7e-132">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="eed7e-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="eed7e-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="eed7e-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="eed7e-134">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span><span class="sxs-lookup"><span data-stu-id="eed7e-134">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="eed7e-135">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="eed7e-135">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="eed7e-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="eed7e-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="eed7e-137">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="eed7e-137">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="eed7e-138">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span><span class="sxs-lookup"><span data-stu-id="eed7e-138">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="eed7e-139">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="eed7e-139">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="eed7e-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span><span class="sxs-lookup"><span data-stu-id="eed7e-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="eed7e-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="eed7e-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="eed7e-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="eed7e-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="eed7e-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span><span class="sxs-lookup"><span data-stu-id="eed7e-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="eed7e-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="eed7e-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="eed7e-145">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="eed7e-145">Linked service properties</span></span>
<span data-ttu-id="eed7e-146">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span><span class="sxs-lookup"><span data-stu-id="eed7e-146">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="eed7e-147">Property</span><span class="sxs-lookup"><span data-stu-id="eed7e-147">Property</span></span> | <span data-ttu-id="eed7e-148">Description</span><span class="sxs-lookup"><span data-stu-id="eed7e-148">Description</span></span> | <span data-ttu-id="eed7e-149">Required</span><span class="sxs-lookup"><span data-stu-id="eed7e-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eed7e-150">type</span><span class="sxs-lookup"><span data-stu-id="eed7e-150">type</span></span> |<span data-ttu-id="eed7e-151">The type property must be set to: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="eed7e-151">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="eed7e-152">Yes</span><span class="sxs-lookup"><span data-stu-id="eed7e-152">Yes</span></span> |
| <span data-ttu-id="eed7e-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="eed7e-153">connectionString</span></span> |<span data-ttu-id="eed7e-154">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="eed7e-154">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="eed7e-155">Only basic authentication is supported.</span><span class="sxs-lookup"><span data-stu-id="eed7e-155">Only basic authentication is supported.</span></span> |<span data-ttu-id="eed7e-156">Yes</span><span class="sxs-lookup"><span data-stu-id="eed7e-156">Yes</span></span> |

> [!IMPORTANT]
> Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.

## <a name="dataset-properties"></a><span data-ttu-id="eed7e-159">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="eed7e-159">Dataset properties</span></span>
<span data-ttu-id="eed7e-160">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="eed7e-160">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="eed7e-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="eed7e-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="eed7e-162">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="eed7e-162">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="eed7e-163">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="eed7e-163">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="eed7e-164">Property</span><span class="sxs-lookup"><span data-stu-id="eed7e-164">Property</span></span> | <span data-ttu-id="eed7e-165">Description</span><span class="sxs-lookup"><span data-stu-id="eed7e-165">Description</span></span> | <span data-ttu-id="eed7e-166">Required</span><span class="sxs-lookup"><span data-stu-id="eed7e-166">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eed7e-167">tableName</span><span class="sxs-lookup"><span data-stu-id="eed7e-167">tableName</span></span> |<span data-ttu-id="eed7e-168">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="eed7e-168">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="eed7e-169">Yes</span><span class="sxs-lookup"><span data-stu-id="eed7e-169">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="eed7e-170">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="eed7e-170">Copy activity properties</span></span>
<span data-ttu-id="eed7e-171">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="eed7e-171">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="eed7e-172">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="eed7e-172">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> The Copy Activity takes only one input and produces only one output.

<span data-ttu-id="eed7e-174">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="eed7e-174">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="eed7e-175">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="eed7e-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="eed7e-176">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="eed7e-176">SqlDWSource</span></span>
<span data-ttu-id="eed7e-177">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="eed7e-177">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="eed7e-178">Property</span><span class="sxs-lookup"><span data-stu-id="eed7e-178">Property</span></span> | <span data-ttu-id="eed7e-179">Description</span><span class="sxs-lookup"><span data-stu-id="eed7e-179">Description</span></span> | <span data-ttu-id="eed7e-180">Allowed values</span><span class="sxs-lookup"><span data-stu-id="eed7e-180">Allowed values</span></span> | <span data-ttu-id="eed7e-181">Required</span><span class="sxs-lookup"><span data-stu-id="eed7e-181">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eed7e-182">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="eed7e-182">sqlReaderQuery</span></span> |<span data-ttu-id="eed7e-183">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="eed7e-183">Use the custom query to read data.</span></span> |<span data-ttu-id="eed7e-184">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="eed7e-184">SQL query string.</span></span> <span data-ttu-id="eed7e-185">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="eed7e-185">For example: select \* from MyTable.</span></span> |<span data-ttu-id="eed7e-186">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-186">No</span></span> |
| <span data-ttu-id="eed7e-187">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="eed7e-187">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="eed7e-188">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="eed7e-188">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="eed7e-189">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="eed7e-189">Name of the stored procedure.</span></span> <span data-ttu-id="eed7e-190">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="eed7e-190">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="eed7e-191">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-191">No</span></span> |
| <span data-ttu-id="eed7e-192">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="eed7e-192">storedProcedureParameters</span></span> |<span data-ttu-id="eed7e-193">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="eed7e-193">Parameters for the stored procedure.</span></span> |<span data-ttu-id="eed7e-194">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="eed7e-194">Name/value pairs.</span></span> <span data-ttu-id="eed7e-195">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="eed7e-195">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="eed7e-196">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-196">No</span></span> |

<span data-ttu-id="eed7e-197">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span><span class="sxs-lookup"><span data-stu-id="eed7e-197">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="eed7e-198">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="eed7e-198">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="eed7e-199">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eed7e-199">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="eed7e-200">Example: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="eed7e-200">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="eed7e-201">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="eed7e-201">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="eed7e-202">SqlDWSource example</span><span class="sxs-lookup"><span data-stu-id="eed7e-202">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="eed7e-203">**The stored procedure definition:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-203">**The stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a><span data-ttu-id="eed7e-204">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="eed7e-204">SqlDWSink</span></span>
<span data-ttu-id="eed7e-205">**SqlDWSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="eed7e-205">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="eed7e-206">Property</span><span class="sxs-lookup"><span data-stu-id="eed7e-206">Property</span></span> | <span data-ttu-id="eed7e-207">Description</span><span class="sxs-lookup"><span data-stu-id="eed7e-207">Description</span></span> | <span data-ttu-id="eed7e-208">Allowed values</span><span class="sxs-lookup"><span data-stu-id="eed7e-208">Allowed values</span></span> | <span data-ttu-id="eed7e-209">Required</span><span class="sxs-lookup"><span data-stu-id="eed7e-209">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eed7e-210">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="eed7e-210">sqlWriterCleanupScript</span></span> |<span data-ttu-id="eed7e-211">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="eed7e-211">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="eed7e-212">For details, see [repeatability section](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="eed7e-212">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="eed7e-213">A query statement.</span><span class="sxs-lookup"><span data-stu-id="eed7e-213">A query statement.</span></span> |<span data-ttu-id="eed7e-214">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-214">No</span></span> |
| <span data-ttu-id="eed7e-215">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="eed7e-215">allowPolyBase</span></span> |<span data-ttu-id="eed7e-216">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span><span class="sxs-lookup"><span data-stu-id="eed7e-216">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="eed7e-217">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="eed7e-217">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="eed7e-218">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span><span class="sxs-lookup"><span data-stu-id="eed7e-218">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="eed7e-219">True</span><span class="sxs-lookup"><span data-stu-id="eed7e-219">True</span></span> <br/><span data-ttu-id="eed7e-220">False (default)</span><span class="sxs-lookup"><span data-stu-id="eed7e-220">False (default)</span></span> |<span data-ttu-id="eed7e-221">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-221">No</span></span> |
| <span data-ttu-id="eed7e-222">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="eed7e-222">polyBaseSettings</span></span> |<span data-ttu-id="eed7e-223">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-223">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="eed7e-224">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-224">No</span></span> |
| <span data-ttu-id="eed7e-225">rejectValue</span><span class="sxs-lookup"><span data-stu-id="eed7e-225">rejectValue</span></span> |<span data-ttu-id="eed7e-226">Specifies the number or percentage of rows that can be rejected before the query fails.</span><span class="sxs-lookup"><span data-stu-id="eed7e-226">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="eed7e-227">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="eed7e-227">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="eed7e-228">0 (default), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="eed7e-228">0 (default), 1, 2, …</span></span> |<span data-ttu-id="eed7e-229">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-229">No</span></span> |
| <span data-ttu-id="eed7e-230">rejectType</span><span class="sxs-lookup"><span data-stu-id="eed7e-230">rejectType</span></span> |<span data-ttu-id="eed7e-231">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span><span class="sxs-lookup"><span data-stu-id="eed7e-231">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="eed7e-232">Value (default), Percentage</span><span class="sxs-lookup"><span data-stu-id="eed7e-232">Value (default), Percentage</span></span> |<span data-ttu-id="eed7e-233">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-233">No</span></span> |
| <span data-ttu-id="eed7e-234">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="eed7e-234">rejectSampleValue</span></span> |<span data-ttu-id="eed7e-235">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span><span class="sxs-lookup"><span data-stu-id="eed7e-235">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="eed7e-236">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="eed7e-236">1, 2, …</span></span> |<span data-ttu-id="eed7e-237">Yes, if **rejectType** is **percentage**</span><span class="sxs-lookup"><span data-stu-id="eed7e-237">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="eed7e-238">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="eed7e-238">useTypeDefault</span></span> |<span data-ttu-id="eed7e-239">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span><span class="sxs-lookup"><span data-stu-id="eed7e-239">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="eed7e-240">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="eed7e-240">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="eed7e-241">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="eed7e-241">True, False (default)</span></span> |<span data-ttu-id="eed7e-242">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-242">No</span></span> |
| <span data-ttu-id="eed7e-243">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="eed7e-243">writeBatchSize</span></span> |<span data-ttu-id="eed7e-244">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="eed7e-244">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="eed7e-245">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="eed7e-245">Integer (number of rows)</span></span> |<span data-ttu-id="eed7e-246">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="eed7e-246">No (default: 10000)</span></span> |
| <span data-ttu-id="eed7e-247">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="eed7e-247">writeBatchTimeout</span></span> |<span data-ttu-id="eed7e-248">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="eed7e-248">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="eed7e-249">timespan</span><span class="sxs-lookup"><span data-stu-id="eed7e-249">timespan</span></span><br/><br/> <span data-ttu-id="eed7e-250">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="eed7e-250">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="eed7e-251">No</span><span class="sxs-lookup"><span data-stu-id="eed7e-251">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="eed7e-252">SqlDWSink example</span><span class="sxs-lookup"><span data-stu-id="eed7e-252">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="eed7e-253">Use PolyBase to load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="eed7e-253">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="eed7e-254">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span><span class="sxs-lookup"><span data-stu-id="eed7e-254">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="eed7e-255">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span><span class="sxs-lookup"><span data-stu-id="eed7e-255">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="eed7e-256">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span><span class="sxs-lookup"><span data-stu-id="eed7e-256">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="eed7e-257">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="eed7e-257">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="eed7e-258">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span><span class="sxs-lookup"><span data-stu-id="eed7e-258">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="eed7e-259">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span><span class="sxs-lookup"><span data-stu-id="eed7e-259">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="eed7e-260">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span><span class="sxs-lookup"><span data-stu-id="eed7e-260">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="eed7e-261">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="eed7e-261">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="eed7e-262">It then loads data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eed7e-262">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="eed7e-263">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eed7e-263">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="eed7e-264">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span><span class="sxs-lookup"><span data-stu-id="eed7e-264">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="eed7e-265">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="eed7e-265">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="eed7e-266">Direct copy using PolyBase</span><span class="sxs-lookup"><span data-stu-id="eed7e-266">Direct copy using PolyBase</span></span>
<span data-ttu-id="eed7e-267">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span><span class="sxs-lookup"><span data-stu-id="eed7e-267">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="eed7e-268">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span><span class="sxs-lookup"><span data-stu-id="eed7e-268">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="eed7e-269">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="eed7e-269">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

<span data-ttu-id="eed7e-271">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span><span class="sxs-lookup"><span data-stu-id="eed7e-271">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="eed7e-272">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-272">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="eed7e-273">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, **ParquetFormat**, or **TextFormat** with the following configurations:</span><span class="sxs-lookup"><span data-stu-id="eed7e-273">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, **ParquetFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="eed7e-274">`rowDelimiter` must be **\n**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-274">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="eed7e-275">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-275">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="eed7e-276">`encodingName` is set to **utf-8**, which is **default** value.</span><span class="sxs-lookup"><span data-stu-id="eed7e-276">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="eed7e-277">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span><span class="sxs-lookup"><span data-stu-id="eed7e-277">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="eed7e-278">`compression` can be **no compression**, **GZip**, or **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-278">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="eed7e-279">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="eed7e-279">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="eed7e-280">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="eed7e-280">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="eed7e-281">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span><span class="sxs-lookup"><span data-stu-id="eed7e-281">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="eed7e-282">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="eed7e-282">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="eed7e-283">There is no `columnMapping` being used in the associated in Copy activity.</span><span class="sxs-lookup"><span data-stu-id="eed7e-283">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="eed7e-284">Staged Copy using PolyBase</span><span class="sxs-lookup"><span data-stu-id="eed7e-284">Staged Copy using PolyBase</span></span>
<span data-ttu-id="eed7e-285">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span><span class="sxs-lookup"><span data-stu-id="eed7e-285">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="eed7e-286">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span><span class="sxs-lookup"><span data-stu-id="eed7e-286">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="eed7e-287">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span><span class="sxs-lookup"><span data-stu-id="eed7e-287">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format. Suggest you upgrade your gateway to the latest to avoid such dependency.
>

<span data-ttu-id="eed7e-290">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="eed7e-290">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="eed7e-291">Best practices when using PolyBase</span><span class="sxs-lookup"><span data-stu-id="eed7e-291">Best practices when using PolyBase</span></span>
<span data-ttu-id="eed7e-292">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="eed7e-292">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="eed7e-293">Required database permission</span><span class="sxs-lookup"><span data-stu-id="eed7e-293">Required database permission</span></span>
<span data-ttu-id="eed7e-294">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span><span class="sxs-lookup"><span data-stu-id="eed7e-294">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="eed7e-295">One way to achieve that is to add that user as a member of "db_owner" role.</span><span class="sxs-lookup"><span data-stu-id="eed7e-295">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="eed7e-296">Learn how to do that by following [this section](../../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="eed7e-296">Learn how to do that by following [this section](../../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="eed7e-297">Row size and data type limitation</span><span class="sxs-lookup"><span data-stu-id="eed7e-297">Row size and data type limitation</span></span>
<span data-ttu-id="eed7e-298">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="eed7e-298">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="eed7e-299">Refer to [here](../../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="eed7e-299">Refer to [here](../../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="eed7e-300">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span><span class="sxs-lookup"><span data-stu-id="eed7e-300">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="eed7e-301">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eed7e-301">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="eed7e-302">SQL Data Warehouse resource class</span><span class="sxs-lookup"><span data-stu-id="eed7e-302">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="eed7e-303">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="eed7e-303">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="eed7e-304">Learn how to do that by following [Change a user resource class example](../../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="eed7e-304">Learn how to do that by following [Change a user resource class example](../../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="eed7e-305">tableName in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="eed7e-305">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="eed7e-306">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span><span class="sxs-lookup"><span data-stu-id="eed7e-306">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="eed7e-307">DB Schema</span><span class="sxs-lookup"><span data-stu-id="eed7e-307">DB Schema</span></span> | <span data-ttu-id="eed7e-308">Table name</span><span class="sxs-lookup"><span data-stu-id="eed7e-308">Table name</span></span> | <span data-ttu-id="eed7e-309">tableName JSON property</span><span class="sxs-lookup"><span data-stu-id="eed7e-309">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eed7e-310">dbo</span><span class="sxs-lookup"><span data-stu-id="eed7e-310">dbo</span></span> |<span data-ttu-id="eed7e-311">MyTable</span><span class="sxs-lookup"><span data-stu-id="eed7e-311">MyTable</span></span> |<span data-ttu-id="eed7e-312">MyTable or dbo.MyTable or [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="eed7e-312">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="eed7e-313">dbo1</span><span class="sxs-lookup"><span data-stu-id="eed7e-313">dbo1</span></span> |<span data-ttu-id="eed7e-314">MyTable</span><span class="sxs-lookup"><span data-stu-id="eed7e-314">MyTable</span></span> |<span data-ttu-id="eed7e-315">dbo1.MyTable or [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="eed7e-315">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="eed7e-316">dbo</span><span class="sxs-lookup"><span data-stu-id="eed7e-316">dbo</span></span> |<span data-ttu-id="eed7e-317">My.Table</span><span class="sxs-lookup"><span data-stu-id="eed7e-317">My.Table</span></span> |<span data-ttu-id="eed7e-318">[My.Table] or [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="eed7e-318">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="eed7e-319">dbo1</span><span class="sxs-lookup"><span data-stu-id="eed7e-319">dbo1</span></span> |<span data-ttu-id="eed7e-320">My.Table</span><span class="sxs-lookup"><span data-stu-id="eed7e-320">My.Table</span></span> |<span data-ttu-id="eed7e-321">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="eed7e-321">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="eed7e-322">If you see the following error, it could be an issue with the value you specified for the tableName property.</span><span class="sxs-lookup"><span data-stu-id="eed7e-322">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="eed7e-323">See the table for the correct way to specify values for the tableName JSON property.</span><span class="sxs-lookup"><span data-stu-id="eed7e-323">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="eed7e-324">Columns with default values</span><span class="sxs-lookup"><span data-stu-id="eed7e-324">Columns with default values</span></span>
<span data-ttu-id="eed7e-325">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span><span class="sxs-lookup"><span data-stu-id="eed7e-325">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="eed7e-326">Say, you have a table with four columns and one of them is defined with a default value.</span><span class="sxs-lookup"><span data-stu-id="eed7e-326">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="eed7e-327">The input data should still contain four columns.</span><span class="sxs-lookup"><span data-stu-id="eed7e-327">The input data should still contain four columns.</span></span> <span data-ttu-id="eed7e-328">Providing a 3-column input dataset would yield an error similar to the following message:</span><span class="sxs-lookup"><span data-stu-id="eed7e-328">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="eed7e-329">NULL value is a special form of default value.</span><span class="sxs-lookup"><span data-stu-id="eed7e-329">NULL value is a special form of default value.</span></span> <span data-ttu-id="eed7e-330">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span><span class="sxs-lookup"><span data-stu-id="eed7e-330">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="eed7e-331">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eed7e-331">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="eed7e-332">Auto table creation</span><span class="sxs-lookup"><span data-stu-id="eed7e-332">Auto table creation</span></span>
<span data-ttu-id="eed7e-333">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span><span class="sxs-lookup"><span data-stu-id="eed7e-333">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="eed7e-334">Data Factory creates the table in the destination store with the same table name in the source data store.</span><span class="sxs-lookup"><span data-stu-id="eed7e-334">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="eed7e-335">The data types for columns are chosen based on the following type mapping.</span><span class="sxs-lookup"><span data-stu-id="eed7e-335">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="eed7e-336">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span><span class="sxs-lookup"><span data-stu-id="eed7e-336">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="eed7e-337">It also uses Round Robin table distribution.</span><span class="sxs-lookup"><span data-stu-id="eed7e-337">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="eed7e-338">Source SQL Database column type</span><span class="sxs-lookup"><span data-stu-id="eed7e-338">Source SQL Database column type</span></span> | <span data-ttu-id="eed7e-339">Destination SQL DW column type (size limitation)</span><span class="sxs-lookup"><span data-stu-id="eed7e-339">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="eed7e-340">Int</span><span class="sxs-lookup"><span data-stu-id="eed7e-340">Int</span></span> | <span data-ttu-id="eed7e-341">Int</span><span class="sxs-lookup"><span data-stu-id="eed7e-341">Int</span></span> |
| <span data-ttu-id="eed7e-342">BigInt</span><span class="sxs-lookup"><span data-stu-id="eed7e-342">BigInt</span></span> | <span data-ttu-id="eed7e-343">BigInt</span><span class="sxs-lookup"><span data-stu-id="eed7e-343">BigInt</span></span> |
| <span data-ttu-id="eed7e-344">SmallInt</span><span class="sxs-lookup"><span data-stu-id="eed7e-344">SmallInt</span></span> | <span data-ttu-id="eed7e-345">SmallInt</span><span class="sxs-lookup"><span data-stu-id="eed7e-345">SmallInt</span></span> |
| <span data-ttu-id="eed7e-346">TinyInt</span><span class="sxs-lookup"><span data-stu-id="eed7e-346">TinyInt</span></span> | <span data-ttu-id="eed7e-347">TinyInt</span><span class="sxs-lookup"><span data-stu-id="eed7e-347">TinyInt</span></span> |
| <span data-ttu-id="eed7e-348">Bit</span><span class="sxs-lookup"><span data-stu-id="eed7e-348">Bit</span></span> | <span data-ttu-id="eed7e-349">Bit</span><span class="sxs-lookup"><span data-stu-id="eed7e-349">Bit</span></span> |
| <span data-ttu-id="eed7e-350">Decimal</span><span class="sxs-lookup"><span data-stu-id="eed7e-350">Decimal</span></span> | <span data-ttu-id="eed7e-351">Decimal</span><span class="sxs-lookup"><span data-stu-id="eed7e-351">Decimal</span></span> |
| <span data-ttu-id="eed7e-352">Numeric</span><span class="sxs-lookup"><span data-stu-id="eed7e-352">Numeric</span></span> | <span data-ttu-id="eed7e-353">Decimal</span><span class="sxs-lookup"><span data-stu-id="eed7e-353">Decimal</span></span> |
| <span data-ttu-id="eed7e-354">Float</span><span class="sxs-lookup"><span data-stu-id="eed7e-354">Float</span></span> | <span data-ttu-id="eed7e-355">Float</span><span class="sxs-lookup"><span data-stu-id="eed7e-355">Float</span></span> |
| <span data-ttu-id="eed7e-356">Money</span><span class="sxs-lookup"><span data-stu-id="eed7e-356">Money</span></span> | <span data-ttu-id="eed7e-357">Money</span><span class="sxs-lookup"><span data-stu-id="eed7e-357">Money</span></span> |
| <span data-ttu-id="eed7e-358">Real</span><span class="sxs-lookup"><span data-stu-id="eed7e-358">Real</span></span> | <span data-ttu-id="eed7e-359">Real</span><span class="sxs-lookup"><span data-stu-id="eed7e-359">Real</span></span> |
| <span data-ttu-id="eed7e-360">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="eed7e-360">SmallMoney</span></span> | <span data-ttu-id="eed7e-361">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="eed7e-361">SmallMoney</span></span> |
| <span data-ttu-id="eed7e-362">Binary</span><span class="sxs-lookup"><span data-stu-id="eed7e-362">Binary</span></span> | <span data-ttu-id="eed7e-363">Binary</span><span class="sxs-lookup"><span data-stu-id="eed7e-363">Binary</span></span> |
| <span data-ttu-id="eed7e-364">Varbinary</span><span class="sxs-lookup"><span data-stu-id="eed7e-364">Varbinary</span></span> | <span data-ttu-id="eed7e-365">Varbinary (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="eed7e-365">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="eed7e-366">Date</span><span class="sxs-lookup"><span data-stu-id="eed7e-366">Date</span></span> | <span data-ttu-id="eed7e-367">Date</span><span class="sxs-lookup"><span data-stu-id="eed7e-367">Date</span></span> |
| <span data-ttu-id="eed7e-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="eed7e-368">DateTime</span></span> | <span data-ttu-id="eed7e-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="eed7e-369">DateTime</span></span> |
| <span data-ttu-id="eed7e-370">DateTime2</span><span class="sxs-lookup"><span data-stu-id="eed7e-370">DateTime2</span></span> | <span data-ttu-id="eed7e-371">DateTime2</span><span class="sxs-lookup"><span data-stu-id="eed7e-371">DateTime2</span></span> |
| <span data-ttu-id="eed7e-372">Time</span><span class="sxs-lookup"><span data-stu-id="eed7e-372">Time</span></span> | <span data-ttu-id="eed7e-373">Time</span><span class="sxs-lookup"><span data-stu-id="eed7e-373">Time</span></span> |
| <span data-ttu-id="eed7e-374">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="eed7e-374">DateTimeOffset</span></span> | <span data-ttu-id="eed7e-375">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="eed7e-375">DateTimeOffset</span></span> |
| <span data-ttu-id="eed7e-376">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="eed7e-376">SmallDateTime</span></span> | <span data-ttu-id="eed7e-377">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="eed7e-377">SmallDateTime</span></span> |
| <span data-ttu-id="eed7e-378">Text</span><span class="sxs-lookup"><span data-stu-id="eed7e-378">Text</span></span> | <span data-ttu-id="eed7e-379">Varchar (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="eed7e-379">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="eed7e-380">NText</span><span class="sxs-lookup"><span data-stu-id="eed7e-380">NText</span></span> | <span data-ttu-id="eed7e-381">NVarChar (up to 4000)</span><span class="sxs-lookup"><span data-stu-id="eed7e-381">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="eed7e-382">Image</span><span class="sxs-lookup"><span data-stu-id="eed7e-382">Image</span></span> | <span data-ttu-id="eed7e-383">VarBinary (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="eed7e-383">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="eed7e-384">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="eed7e-384">UniqueIdentifier</span></span> | <span data-ttu-id="eed7e-385">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="eed7e-385">UniqueIdentifier</span></span> |
| <span data-ttu-id="eed7e-386">Char</span><span class="sxs-lookup"><span data-stu-id="eed7e-386">Char</span></span> | <span data-ttu-id="eed7e-387">Char</span><span class="sxs-lookup"><span data-stu-id="eed7e-387">Char</span></span> |
| <span data-ttu-id="eed7e-388">NChar</span><span class="sxs-lookup"><span data-stu-id="eed7e-388">NChar</span></span> | <span data-ttu-id="eed7e-389">NChar</span><span class="sxs-lookup"><span data-stu-id="eed7e-389">NChar</span></span> |
| <span data-ttu-id="eed7e-390">VarChar</span><span class="sxs-lookup"><span data-stu-id="eed7e-390">VarChar</span></span> | <span data-ttu-id="eed7e-391">VarChar (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="eed7e-391">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="eed7e-392">NVarChar</span><span class="sxs-lookup"><span data-stu-id="eed7e-392">NVarChar</span></span> | <span data-ttu-id="eed7e-393">NVarChar (up to 4000)</span><span class="sxs-lookup"><span data-stu-id="eed7e-393">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="eed7e-394">Xml</span><span class="sxs-lookup"><span data-stu-id="eed7e-394">Xml</span></span> | <span data-ttu-id="eed7e-395">Varchar (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="eed7e-395">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="eed7e-396">Type mapping for Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="eed7e-396">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="eed7e-397">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="eed7e-397">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="eed7e-398">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="eed7e-398">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="eed7e-399">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="eed7e-399">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="eed7e-400">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="eed7e-400">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="eed7e-401">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="eed7e-401">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="eed7e-402">SQL Server Database Engine type</span><span class="sxs-lookup"><span data-stu-id="eed7e-402">SQL Server Database Engine type</span></span> | <span data-ttu-id="eed7e-403">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="eed7e-403">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="eed7e-404">bigint</span><span class="sxs-lookup"><span data-stu-id="eed7e-404">bigint</span></span> |<span data-ttu-id="eed7e-405">Int64</span><span class="sxs-lookup"><span data-stu-id="eed7e-405">Int64</span></span> |
| <span data-ttu-id="eed7e-406">binary</span><span class="sxs-lookup"><span data-stu-id="eed7e-406">binary</span></span> |<span data-ttu-id="eed7e-407">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-407">Byte[]</span></span> |
| <span data-ttu-id="eed7e-408">bit</span><span class="sxs-lookup"><span data-stu-id="eed7e-408">bit</span></span> |<span data-ttu-id="eed7e-409">Boolean</span><span class="sxs-lookup"><span data-stu-id="eed7e-409">Boolean</span></span> |
| <span data-ttu-id="eed7e-410">char</span><span class="sxs-lookup"><span data-stu-id="eed7e-410">char</span></span> |<span data-ttu-id="eed7e-411">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-411">String, Char[]</span></span> |
| <span data-ttu-id="eed7e-412">date</span><span class="sxs-lookup"><span data-stu-id="eed7e-412">date</span></span> |<span data-ttu-id="eed7e-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="eed7e-413">DateTime</span></span> |
| <span data-ttu-id="eed7e-414">Datetime</span><span class="sxs-lookup"><span data-stu-id="eed7e-414">Datetime</span></span> |<span data-ttu-id="eed7e-415">DateTime</span><span class="sxs-lookup"><span data-stu-id="eed7e-415">DateTime</span></span> |
| <span data-ttu-id="eed7e-416">datetime2</span><span class="sxs-lookup"><span data-stu-id="eed7e-416">datetime2</span></span> |<span data-ttu-id="eed7e-417">DateTime</span><span class="sxs-lookup"><span data-stu-id="eed7e-417">DateTime</span></span> |
| <span data-ttu-id="eed7e-418">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="eed7e-418">Datetimeoffset</span></span> |<span data-ttu-id="eed7e-419">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="eed7e-419">DateTimeOffset</span></span> |
| <span data-ttu-id="eed7e-420">Decimal</span><span class="sxs-lookup"><span data-stu-id="eed7e-420">Decimal</span></span> |<span data-ttu-id="eed7e-421">Decimal</span><span class="sxs-lookup"><span data-stu-id="eed7e-421">Decimal</span></span> |
| <span data-ttu-id="eed7e-422">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="eed7e-422">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="eed7e-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-423">Byte[]</span></span> |
| <span data-ttu-id="eed7e-424">Float</span><span class="sxs-lookup"><span data-stu-id="eed7e-424">Float</span></span> |<span data-ttu-id="eed7e-425">Double</span><span class="sxs-lookup"><span data-stu-id="eed7e-425">Double</span></span> |
| <span data-ttu-id="eed7e-426">image</span><span class="sxs-lookup"><span data-stu-id="eed7e-426">image</span></span> |<span data-ttu-id="eed7e-427">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-427">Byte[]</span></span> |
| <span data-ttu-id="eed7e-428">int</span><span class="sxs-lookup"><span data-stu-id="eed7e-428">int</span></span> |<span data-ttu-id="eed7e-429">Int32</span><span class="sxs-lookup"><span data-stu-id="eed7e-429">Int32</span></span> |
| <span data-ttu-id="eed7e-430">money</span><span class="sxs-lookup"><span data-stu-id="eed7e-430">money</span></span> |<span data-ttu-id="eed7e-431">Decimal</span><span class="sxs-lookup"><span data-stu-id="eed7e-431">Decimal</span></span> |
| <span data-ttu-id="eed7e-432">nchar</span><span class="sxs-lookup"><span data-stu-id="eed7e-432">nchar</span></span> |<span data-ttu-id="eed7e-433">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-433">String, Char[]</span></span> |
| <span data-ttu-id="eed7e-434">ntext</span><span class="sxs-lookup"><span data-stu-id="eed7e-434">ntext</span></span> |<span data-ttu-id="eed7e-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-435">String, Char[]</span></span> |
| <span data-ttu-id="eed7e-436">numeric</span><span class="sxs-lookup"><span data-stu-id="eed7e-436">numeric</span></span> |<span data-ttu-id="eed7e-437">Decimal</span><span class="sxs-lookup"><span data-stu-id="eed7e-437">Decimal</span></span> |
| <span data-ttu-id="eed7e-438">nvarchar</span><span class="sxs-lookup"><span data-stu-id="eed7e-438">nvarchar</span></span> |<span data-ttu-id="eed7e-439">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-439">String, Char[]</span></span> |
| <span data-ttu-id="eed7e-440">real</span><span class="sxs-lookup"><span data-stu-id="eed7e-440">real</span></span> |<span data-ttu-id="eed7e-441">Single</span><span class="sxs-lookup"><span data-stu-id="eed7e-441">Single</span></span> |
| <span data-ttu-id="eed7e-442">rowversion</span><span class="sxs-lookup"><span data-stu-id="eed7e-442">rowversion</span></span> |<span data-ttu-id="eed7e-443">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-443">Byte[]</span></span> |
| <span data-ttu-id="eed7e-444">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="eed7e-444">smalldatetime</span></span> |<span data-ttu-id="eed7e-445">DateTime</span><span class="sxs-lookup"><span data-stu-id="eed7e-445">DateTime</span></span> |
| <span data-ttu-id="eed7e-446">smallint</span><span class="sxs-lookup"><span data-stu-id="eed7e-446">smallint</span></span> |<span data-ttu-id="eed7e-447">Int16</span><span class="sxs-lookup"><span data-stu-id="eed7e-447">Int16</span></span> |
| <span data-ttu-id="eed7e-448">smallmoney</span><span class="sxs-lookup"><span data-stu-id="eed7e-448">smallmoney</span></span> |<span data-ttu-id="eed7e-449">Decimal</span><span class="sxs-lookup"><span data-stu-id="eed7e-449">Decimal</span></span> |
| <span data-ttu-id="eed7e-450">sql_variant</span><span class="sxs-lookup"><span data-stu-id="eed7e-450">sql_variant</span></span> |<span data-ttu-id="eed7e-451">Object \*</span><span class="sxs-lookup"><span data-stu-id="eed7e-451">Object \*</span></span> |
| <span data-ttu-id="eed7e-452">text</span><span class="sxs-lookup"><span data-stu-id="eed7e-452">text</span></span> |<span data-ttu-id="eed7e-453">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-453">String, Char[]</span></span> |
| <span data-ttu-id="eed7e-454">time</span><span class="sxs-lookup"><span data-stu-id="eed7e-454">time</span></span> |<span data-ttu-id="eed7e-455">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="eed7e-455">TimeSpan</span></span> |
| <span data-ttu-id="eed7e-456">timestamp</span><span class="sxs-lookup"><span data-stu-id="eed7e-456">timestamp</span></span> |<span data-ttu-id="eed7e-457">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-457">Byte[]</span></span> |
| <span data-ttu-id="eed7e-458">tinyint</span><span class="sxs-lookup"><span data-stu-id="eed7e-458">tinyint</span></span> |<span data-ttu-id="eed7e-459">Byte</span><span class="sxs-lookup"><span data-stu-id="eed7e-459">Byte</span></span> |
| <span data-ttu-id="eed7e-460">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="eed7e-460">uniqueidentifier</span></span> |<span data-ttu-id="eed7e-461">Guid</span><span class="sxs-lookup"><span data-stu-id="eed7e-461">Guid</span></span> |
| <span data-ttu-id="eed7e-462">varbinary</span><span class="sxs-lookup"><span data-stu-id="eed7e-462">varbinary</span></span> |<span data-ttu-id="eed7e-463">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-463">Byte[]</span></span> |
| <span data-ttu-id="eed7e-464">varchar</span><span class="sxs-lookup"><span data-stu-id="eed7e-464">varchar</span></span> |<span data-ttu-id="eed7e-465">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="eed7e-465">String, Char[]</span></span> |
| <span data-ttu-id="eed7e-466">xml</span><span class="sxs-lookup"><span data-stu-id="eed7e-466">xml</span></span> |<span data-ttu-id="eed7e-467">Xml</span><span class="sxs-lookup"><span data-stu-id="eed7e-467">Xml</span></span> |

<span data-ttu-id="eed7e-468">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span><span class="sxs-lookup"><span data-stu-id="eed7e-468">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="eed7e-469">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="eed7e-469">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="eed7e-470">JSON examples for copying data to and from SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="eed7e-470">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="eed7e-471">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="eed7e-471">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="eed7e-472">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="eed7e-472">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="eed7e-473">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="eed7e-473">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="eed7e-474">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="eed7e-474">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="eed7e-475">The sample defines the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="eed7e-475">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="eed7e-476">A linked service of type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-476">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="eed7e-477">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-477">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="eed7e-478">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-478">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="eed7e-479">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-479">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="eed7e-480">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-480">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="eed7e-481">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="eed7e-481">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="eed7e-482">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="eed7e-482">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="eed7e-483">**Azure SQL Data Warehouse linked service:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-483">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="eed7e-484">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-484">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="eed7e-485">**Azure SQL Data Warehouse input dataset:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-485">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="eed7e-486">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="eed7e-486">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="eed7e-487">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="eed7e-487">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="eed7e-488">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-488">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="eed7e-489">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="eed7e-489">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="eed7e-490">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="eed7e-490">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="eed7e-491">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="eed7e-491">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="eed7e-492">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-492">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="eed7e-493">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="eed7e-493">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="eed7e-494">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-494">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="eed7e-495">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="eed7e-495">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> In the example, **sqlReaderQuery** is specified for the SqlDWSource. The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.
>
> Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).
>
> If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse. If the dataset definition does not have the structure, all columns are selected from the table.
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="eed7e-501">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="eed7e-501">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="eed7e-502">The sample defines the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="eed7e-502">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="eed7e-503">A linked service of type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-503">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="eed7e-504">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-504">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="eed7e-505">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-505">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="eed7e-506">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-506">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="eed7e-507">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="eed7e-507">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="eed7e-508">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span><span class="sxs-lookup"><span data-stu-id="eed7e-508">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="eed7e-509">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="eed7e-509">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="eed7e-510">**Azure SQL Data Warehouse linked service:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-510">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="eed7e-511">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-511">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="eed7e-512">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-512">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="eed7e-513">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="eed7e-513">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="eed7e-514">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="eed7e-514">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="eed7e-515">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="eed7e-515">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="eed7e-516">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="eed7e-516">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="eed7e-517">**Azure SQL Data Warehouse output dataset:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-517">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="eed7e-518">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eed7e-518">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="eed7e-519">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="eed7e-519">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="eed7e-520">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="eed7e-520">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="eed7e-521">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="eed7e-521">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="eed7e-522">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="eed7e-522">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="eed7e-523">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="eed7e-523">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="eed7e-524">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span><span class="sxs-lookup"><span data-stu-id="eed7e-524">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="eed7e-525">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="eed7e-525">Performance and Tuning</span></span>
<span data-ttu-id="eed7e-526">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="eed7e-526">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
