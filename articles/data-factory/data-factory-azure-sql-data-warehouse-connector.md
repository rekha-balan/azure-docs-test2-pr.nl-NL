---
title: Move data to/from Azure SQL Data Warehouse | Microsoft Docs
description: Learn how to move data to/from Azure SQL Data Warehouse using Azure Data Factory
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: jingwang
ms.openlocfilehash: c491e8c8ac994ff5c303499a100f0a5307760f8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562899"
---
# <a name="move-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="f14a2-103">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f14a2-103">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="f14a2-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f14a2-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="f14a2-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

<span data-ttu-id="f14a2-106">You can copy data from any supported source data store to Azure SQL Data Warehouse or from Azure SQL Warehouse to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f14a2-106">You can copy data from any supported source data store to Azure SQL Data Warehouse or from Azure SQL Warehouse to any supported sink data store.</span></span> <span data-ttu-id="f14a2-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="f14a2-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span>

> [!TIP]
> <span data-ttu-id="f14a2-108">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-108">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f14a2-109">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span><span class="sxs-lookup"><span data-stu-id="f14a2-109">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="f14a2-110">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="f14a2-110">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="f14a2-111">Supported authentication type</span><span class="sxs-lookup"><span data-stu-id="f14a2-111">Supported authentication type</span></span>
<span data-ttu-id="f14a2-112">Azure SQL Data Warehouse connector support basic authentication.</span><span class="sxs-lookup"><span data-stu-id="f14a2-112">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f14a2-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="f14a2-113">Getting started</span></span>
<span data-ttu-id="f14a2-114">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="f14a2-114">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="f14a2-115">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="f14a2-115">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="f14a2-116">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="f14a2-116">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

> [!TIP]
> <span data-ttu-id="f14a2-117">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span><span class="sxs-lookup"><span data-stu-id="f14a2-117">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="f14a2-118">See [Auto table creation](#auto-table-creation) for details.</span><span class="sxs-lookup"><span data-stu-id="f14a2-118">See [Auto table creation](#auto-table-creation) for details.</span></span>

<span data-ttu-id="f14a2-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="f14a2-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f14a2-120">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="f14a2-120">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="f14a2-121">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="f14a2-121">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="f14a2-122">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f14a2-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="f14a2-123">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="f14a2-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="f14a2-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="f14a2-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="f14a2-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="f14a2-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="f14a2-126">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="f14a2-126">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="f14a2-127">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="f14a2-127">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples) section of this article.</span></span>

<span data-ttu-id="f14a2-128">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="f14a2-128">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f14a2-129">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f14a2-129">Linked service properties</span></span>
<span data-ttu-id="f14a2-130">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span><span class="sxs-lookup"><span data-stu-id="f14a2-130">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="f14a2-131">Property</span><span class="sxs-lookup"><span data-stu-id="f14a2-131">Property</span></span> | <span data-ttu-id="f14a2-132">Description</span><span class="sxs-lookup"><span data-stu-id="f14a2-132">Description</span></span> | <span data-ttu-id="f14a2-133">Required</span><span class="sxs-lookup"><span data-stu-id="f14a2-133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f14a2-134">type</span><span class="sxs-lookup"><span data-stu-id="f14a2-134">type</span></span> |<span data-ttu-id="f14a2-135">The type property must be set to: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="f14a2-135">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="f14a2-136">Yes</span><span class="sxs-lookup"><span data-stu-id="f14a2-136">Yes</span></span> |
| <span data-ttu-id="f14a2-137">connectionString</span><span class="sxs-lookup"><span data-stu-id="f14a2-137">connectionString</span></span> |<span data-ttu-id="f14a2-138">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="f14a2-138">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="f14a2-139">Only basic authentication is supported.</span><span class="sxs-lookup"><span data-stu-id="f14a2-139">Only basic authentication is supported.</span></span> |<span data-ttu-id="f14a2-140">Yes</span><span class="sxs-lookup"><span data-stu-id="f14a2-140">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f14a2-141">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="f14a2-141">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="f14a2-142">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-142">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="f14a2-143">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f14a2-143">Dataset properties</span></span>
<span data-ttu-id="f14a2-144">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="f14a2-144">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f14a2-145">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="f14a2-145">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f14a2-146">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="f14a2-146">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f14a2-147">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="f14a2-147">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="f14a2-148">Property</span><span class="sxs-lookup"><span data-stu-id="f14a2-148">Property</span></span> | <span data-ttu-id="f14a2-149">Description</span><span class="sxs-lookup"><span data-stu-id="f14a2-149">Description</span></span> | <span data-ttu-id="f14a2-150">Required</span><span class="sxs-lookup"><span data-stu-id="f14a2-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f14a2-151">tableName</span><span class="sxs-lookup"><span data-stu-id="f14a2-151">tableName</span></span> |<span data-ttu-id="f14a2-152">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="f14a2-152">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="f14a2-153">Yes</span><span class="sxs-lookup"><span data-stu-id="f14a2-153">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f14a2-154">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f14a2-154">Copy activity properties</span></span>
<span data-ttu-id="f14a2-155">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="f14a2-155">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f14a2-156">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="f14a2-156">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="f14a2-157">The Copy Activity takes only one input and produces only one output.</span><span class="sxs-lookup"><span data-stu-id="f14a2-157">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="f14a2-158">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="f14a2-158">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="f14a2-159">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="f14a2-159">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="f14a2-160">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="f14a2-160">SqlDWSource</span></span>
<span data-ttu-id="f14a2-161">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="f14a2-161">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="f14a2-162">Property</span><span class="sxs-lookup"><span data-stu-id="f14a2-162">Property</span></span> | <span data-ttu-id="f14a2-163">Description</span><span class="sxs-lookup"><span data-stu-id="f14a2-163">Description</span></span> | <span data-ttu-id="f14a2-164">Allowed values</span><span class="sxs-lookup"><span data-stu-id="f14a2-164">Allowed values</span></span> | <span data-ttu-id="f14a2-165">Required</span><span class="sxs-lookup"><span data-stu-id="f14a2-165">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f14a2-166">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="f14a2-166">sqlReaderQuery</span></span> |<span data-ttu-id="f14a2-167">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="f14a2-167">Use the custom query to read data.</span></span> |<span data-ttu-id="f14a2-168">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="f14a2-168">SQL query string.</span></span> <span data-ttu-id="f14a2-169">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="f14a2-169">For example: select \* from MyTable.</span></span> |<span data-ttu-id="f14a2-170">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-170">No</span></span> |
| <span data-ttu-id="f14a2-171">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="f14a2-171">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="f14a2-172">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="f14a2-172">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="f14a2-173">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f14a2-173">Name of the stored procedure.</span></span> <span data-ttu-id="f14a2-174">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f14a2-174">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="f14a2-175">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-175">No</span></span> |
| <span data-ttu-id="f14a2-176">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="f14a2-176">storedProcedureParameters</span></span> |<span data-ttu-id="f14a2-177">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f14a2-177">Parameters for the stored procedure.</span></span> |<span data-ttu-id="f14a2-178">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="f14a2-178">Name/value pairs.</span></span> <span data-ttu-id="f14a2-179">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="f14a2-179">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="f14a2-180">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-180">No</span></span> |

<span data-ttu-id="f14a2-181">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span><span class="sxs-lookup"><span data-stu-id="f14a2-181">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="f14a2-182">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="f14a2-182">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="f14a2-183">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-183">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f14a2-184">Example: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="f14a2-184">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="f14a2-185">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="f14a2-185">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="f14a2-186">SqlDWSource example</span><span class="sxs-lookup"><span data-stu-id="f14a2-186">SqlDWSource example</span></span>

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
<span data-ttu-id="f14a2-187">**The stored procedure definition:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-187">**The stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="f14a2-188">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="f14a2-188">SqlDWSink</span></span>
<span data-ttu-id="f14a2-189">**SqlDWSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="f14a2-189">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="f14a2-190">Property</span><span class="sxs-lookup"><span data-stu-id="f14a2-190">Property</span></span> | <span data-ttu-id="f14a2-191">Description</span><span class="sxs-lookup"><span data-stu-id="f14a2-191">Description</span></span> | <span data-ttu-id="f14a2-192">Allowed values</span><span class="sxs-lookup"><span data-stu-id="f14a2-192">Allowed values</span></span> | <span data-ttu-id="f14a2-193">Required</span><span class="sxs-lookup"><span data-stu-id="f14a2-193">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f14a2-194">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="f14a2-194">sqlWriterCleanupScript</span></span> |<span data-ttu-id="f14a2-195">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="f14a2-195">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="f14a2-196">For details, see [repeatability section](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="f14a2-196">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="f14a2-197">A query statement.</span><span class="sxs-lookup"><span data-stu-id="f14a2-197">A query statement.</span></span> |<span data-ttu-id="f14a2-198">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-198">No</span></span> |
| <span data-ttu-id="f14a2-199">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="f14a2-199">allowPolyBase</span></span> |<span data-ttu-id="f14a2-200">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span><span class="sxs-lookup"><span data-stu-id="f14a2-200">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="f14a2-201">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="f14a2-201">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="f14a2-202">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span><span class="sxs-lookup"><span data-stu-id="f14a2-202">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="f14a2-203">True</span><span class="sxs-lookup"><span data-stu-id="f14a2-203">True</span></span> <br/><span data-ttu-id="f14a2-204">False (default)</span><span class="sxs-lookup"><span data-stu-id="f14a2-204">False (default)</span></span> |<span data-ttu-id="f14a2-205">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-205">No</span></span> |
| <span data-ttu-id="f14a2-206">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="f14a2-206">polyBaseSettings</span></span> |<span data-ttu-id="f14a2-207">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="f14a2-207">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="f14a2-208">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-208">No</span></span> |
| <span data-ttu-id="f14a2-209">rejectValue</span><span class="sxs-lookup"><span data-stu-id="f14a2-209">rejectValue</span></span> |<span data-ttu-id="f14a2-210">Specifies the number or percentage of rows that can be rejected before the query fails.</span><span class="sxs-lookup"><span data-stu-id="f14a2-210">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="f14a2-211">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="f14a2-211">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="f14a2-212">0 (default), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="f14a2-212">0 (default), 1, 2, …</span></span> |<span data-ttu-id="f14a2-213">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-213">No</span></span> |
| <span data-ttu-id="f14a2-214">rejectType</span><span class="sxs-lookup"><span data-stu-id="f14a2-214">rejectType</span></span> |<span data-ttu-id="f14a2-215">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span><span class="sxs-lookup"><span data-stu-id="f14a2-215">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="f14a2-216">Value (default), Percentage</span><span class="sxs-lookup"><span data-stu-id="f14a2-216">Value (default), Percentage</span></span> |<span data-ttu-id="f14a2-217">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-217">No</span></span> |
| <span data-ttu-id="f14a2-218">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="f14a2-218">rejectSampleValue</span></span> |<span data-ttu-id="f14a2-219">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span><span class="sxs-lookup"><span data-stu-id="f14a2-219">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="f14a2-220">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="f14a2-220">1, 2, …</span></span> |<span data-ttu-id="f14a2-221">Yes, if **rejectType** is **percentage**</span><span class="sxs-lookup"><span data-stu-id="f14a2-221">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="f14a2-222">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="f14a2-222">useTypeDefault</span></span> |<span data-ttu-id="f14a2-223">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span><span class="sxs-lookup"><span data-stu-id="f14a2-223">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="f14a2-224">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="f14a2-224">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="f14a2-225">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="f14a2-225">True, False (default)</span></span> |<span data-ttu-id="f14a2-226">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-226">No</span></span> |
| <span data-ttu-id="f14a2-227">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f14a2-227">writeBatchSize</span></span> |<span data-ttu-id="f14a2-228">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f14a2-228">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="f14a2-229">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="f14a2-229">Integer (number of rows)</span></span> |<span data-ttu-id="f14a2-230">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="f14a2-230">No (default: 10000)</span></span> |
| <span data-ttu-id="f14a2-231">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="f14a2-231">writeBatchTimeout</span></span> |<span data-ttu-id="f14a2-232">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="f14a2-232">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="f14a2-233">timespan</span><span class="sxs-lookup"><span data-stu-id="f14a2-233">timespan</span></span><br/><br/> <span data-ttu-id="f14a2-234">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="f14a2-234">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="f14a2-235">No</span><span class="sxs-lookup"><span data-stu-id="f14a2-235">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="f14a2-236">SqlDWSink example</span><span class="sxs-lookup"><span data-stu-id="f14a2-236">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="f14a2-237">Use PolyBase to load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f14a2-237">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f14a2-238">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span><span class="sxs-lookup"><span data-stu-id="f14a2-238">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="f14a2-239">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span><span class="sxs-lookup"><span data-stu-id="f14a2-239">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="f14a2-240">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span><span class="sxs-lookup"><span data-stu-id="f14a2-240">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="f14a2-241">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="f14a2-241">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="f14a2-242">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f14a2-242">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="f14a2-243">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span><span class="sxs-lookup"><span data-stu-id="f14a2-243">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="f14a2-244">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span><span class="sxs-lookup"><span data-stu-id="f14a2-244">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="f14a2-245">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="f14a2-245">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="f14a2-246">It then loads data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-246">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="f14a2-247">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-247">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f14a2-248">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span><span class="sxs-lookup"><span data-stu-id="f14a2-248">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="f14a2-249">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="f14a2-249">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="f14a2-250">Direct copy using PolyBase</span><span class="sxs-lookup"><span data-stu-id="f14a2-250">Direct copy using PolyBase</span></span>
<span data-ttu-id="f14a2-251">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span><span class="sxs-lookup"><span data-stu-id="f14a2-251">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="f14a2-252">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f14a2-252">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="f14a2-253">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="f14a2-253">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="f14a2-254">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="f14a2-254">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="f14a2-255">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span><span class="sxs-lookup"><span data-stu-id="f14a2-255">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="f14a2-256">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span><span class="sxs-lookup"><span data-stu-id="f14a2-256">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="f14a2-257">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span><span class="sxs-lookup"><span data-stu-id="f14a2-257">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="f14a2-258">`rowDelimiter` must be **\n**.</span><span class="sxs-lookup"><span data-stu-id="f14a2-258">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="f14a2-259">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="f14a2-259">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="f14a2-260">`encodingName` is set to **utf-8**, which is **default** value.</span><span class="sxs-lookup"><span data-stu-id="f14a2-260">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="f14a2-261">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span><span class="sxs-lookup"><span data-stu-id="f14a2-261">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="f14a2-262">`compression` can be **no compression**, **GZip**, or **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="f14a2-262">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="f14a2-263">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f14a2-263">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="f14a2-264">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f14a2-264">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="f14a2-265">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span><span class="sxs-lookup"><span data-stu-id="f14a2-265">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="f14a2-266">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="f14a2-266">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="f14a2-267">There is no `columnMapping` being used in the associated in Copy activity.</span><span class="sxs-lookup"><span data-stu-id="f14a2-267">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="f14a2-268">Staged Copy using PolyBase</span><span class="sxs-lookup"><span data-stu-id="f14a2-268">Staged Copy using PolyBase</span></span>
<span data-ttu-id="f14a2-269">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span><span class="sxs-lookup"><span data-stu-id="f14a2-269">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="f14a2-270">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean up your temp data from the Blob storage.</span><span class="sxs-lookup"><span data-stu-id="f14a2-270">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean up your temp data from the Blob storage.</span></span> <span data-ttu-id="f14a2-271">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span><span class="sxs-lookup"><span data-stu-id="f14a2-271">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="f14a2-272">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span><span class="sxs-lookup"><span data-stu-id="f14a2-272">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="f14a2-273">Suggest you upgrade your gateway to the latest to avoid such dependency.</span><span class="sxs-lookup"><span data-stu-id="f14a2-273">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="f14a2-274">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="f14a2-274">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="f14a2-275">Best practices when using PolyBase</span><span class="sxs-lookup"><span data-stu-id="f14a2-275">Best practices when using PolyBase</span></span>
<span data-ttu-id="f14a2-276">Below is supplementary to the generic [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="f14a2-276">Below is supplementary to the generic [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="f14a2-277">Required database permission</span><span class="sxs-lookup"><span data-stu-id="f14a2-277">Required database permission</span></span>
<span data-ttu-id="f14a2-278">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span><span class="sxs-lookup"><span data-stu-id="f14a2-278">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="f14a2-279">One way to achieve that is to add that user as a member of "db_owner" role.</span><span class="sxs-lookup"><span data-stu-id="f14a2-279">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="f14a2-280">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="f14a2-280">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="f14a2-281">Row size and data type limitation</span><span class="sxs-lookup"><span data-stu-id="f14a2-281">Row size and data type limitation</span></span>
<span data-ttu-id="f14a2-282">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="f14a2-282">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="f14a2-283">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="f14a2-283">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="f14a2-284">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span><span class="sxs-lookup"><span data-stu-id="f14a2-284">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="f14a2-285">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-285">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="f14a2-286">SQL Data Warehouse resource class</span><span class="sxs-lookup"><span data-stu-id="f14a2-286">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="f14a2-287">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f14a2-287">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="f14a2-288">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#change-a-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="f14a2-288">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#change-a-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="f14a2-289">tableName in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f14a2-289">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f14a2-290">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span><span class="sxs-lookup"><span data-stu-id="f14a2-290">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="f14a2-291">DB Schema</span><span class="sxs-lookup"><span data-stu-id="f14a2-291">DB Schema</span></span> | <span data-ttu-id="f14a2-292">Table name</span><span class="sxs-lookup"><span data-stu-id="f14a2-292">Table name</span></span> | <span data-ttu-id="f14a2-293">tableName JSON property</span><span class="sxs-lookup"><span data-stu-id="f14a2-293">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f14a2-294">dbo</span><span class="sxs-lookup"><span data-stu-id="f14a2-294">dbo</span></span> |<span data-ttu-id="f14a2-295">MyTable</span><span class="sxs-lookup"><span data-stu-id="f14a2-295">MyTable</span></span> |<span data-ttu-id="f14a2-296">MyTable or dbo.MyTable or [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="f14a2-296">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="f14a2-297">dbo1</span><span class="sxs-lookup"><span data-stu-id="f14a2-297">dbo1</span></span> |<span data-ttu-id="f14a2-298">MyTable</span><span class="sxs-lookup"><span data-stu-id="f14a2-298">MyTable</span></span> |<span data-ttu-id="f14a2-299">dbo1.MyTable or [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="f14a2-299">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="f14a2-300">dbo</span><span class="sxs-lookup"><span data-stu-id="f14a2-300">dbo</span></span> |<span data-ttu-id="f14a2-301">My.Table</span><span class="sxs-lookup"><span data-stu-id="f14a2-301">My.Table</span></span> |<span data-ttu-id="f14a2-302">[My.Table] or [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="f14a2-302">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="f14a2-303">dbo1</span><span class="sxs-lookup"><span data-stu-id="f14a2-303">dbo1</span></span> |<span data-ttu-id="f14a2-304">My.Table</span><span class="sxs-lookup"><span data-stu-id="f14a2-304">My.Table</span></span> |<span data-ttu-id="f14a2-305">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="f14a2-305">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="f14a2-306">If you see the following error, it could be an issue with the value you specified for the tableName property.</span><span class="sxs-lookup"><span data-stu-id="f14a2-306">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="f14a2-307">See the table for the correct way to specify values for the tableName JSON property.</span><span class="sxs-lookup"><span data-stu-id="f14a2-307">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="f14a2-308">Columns with default values</span><span class="sxs-lookup"><span data-stu-id="f14a2-308">Columns with default values</span></span>
<span data-ttu-id="f14a2-309">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span><span class="sxs-lookup"><span data-stu-id="f14a2-309">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="f14a2-310">Say, you have a table with four columns and one of them is defined with a default value.</span><span class="sxs-lookup"><span data-stu-id="f14a2-310">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="f14a2-311">The input data should still contain four columns.</span><span class="sxs-lookup"><span data-stu-id="f14a2-311">The input data should still contain four columns.</span></span> <span data-ttu-id="f14a2-312">Providing a 3-column input dataset would yield an error similar to the following message:</span><span class="sxs-lookup"><span data-stu-id="f14a2-312">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="f14a2-313">NULL value is a special form of default value.</span><span class="sxs-lookup"><span data-stu-id="f14a2-313">NULL value is a special form of default value.</span></span> <span data-ttu-id="f14a2-314">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span><span class="sxs-lookup"><span data-stu-id="f14a2-314">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="f14a2-315">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-315">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="f14a2-316">Auto table creation</span><span class="sxs-lookup"><span data-stu-id="f14a2-316">Auto table creation</span></span>
<span data-ttu-id="f14a2-317">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span><span class="sxs-lookup"><span data-stu-id="f14a2-317">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="f14a2-318">Data Factory creates the table in the destination store with the same table name in the source data store.</span><span class="sxs-lookup"><span data-stu-id="f14a2-318">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="f14a2-319">The data types for columns are chosen based on the following type mapping.</span><span class="sxs-lookup"><span data-stu-id="f14a2-319">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="f14a2-320">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span><span class="sxs-lookup"><span data-stu-id="f14a2-320">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="f14a2-321">It also uses Round Robin table distribution.</span><span class="sxs-lookup"><span data-stu-id="f14a2-321">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="f14a2-322">Source SQL Database column type</span><span class="sxs-lookup"><span data-stu-id="f14a2-322">Source SQL Database column type</span></span> | <span data-ttu-id="f14a2-323">Destination SQL DW column type (size limitation)</span><span class="sxs-lookup"><span data-stu-id="f14a2-323">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="f14a2-324">Int</span><span class="sxs-lookup"><span data-stu-id="f14a2-324">Int</span></span> | <span data-ttu-id="f14a2-325">Int</span><span class="sxs-lookup"><span data-stu-id="f14a2-325">Int</span></span> |
| <span data-ttu-id="f14a2-326">BigInt</span><span class="sxs-lookup"><span data-stu-id="f14a2-326">BigInt</span></span> | <span data-ttu-id="f14a2-327">BigInt</span><span class="sxs-lookup"><span data-stu-id="f14a2-327">BigInt</span></span> |
| <span data-ttu-id="f14a2-328">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f14a2-328">SmallInt</span></span> | <span data-ttu-id="f14a2-329">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f14a2-329">SmallInt</span></span> |
| <span data-ttu-id="f14a2-330">TinyInt</span><span class="sxs-lookup"><span data-stu-id="f14a2-330">TinyInt</span></span> | <span data-ttu-id="f14a2-331">TinyInt</span><span class="sxs-lookup"><span data-stu-id="f14a2-331">TinyInt</span></span> |
| <span data-ttu-id="f14a2-332">Bit</span><span class="sxs-lookup"><span data-stu-id="f14a2-332">Bit</span></span> | <span data-ttu-id="f14a2-333">Bit</span><span class="sxs-lookup"><span data-stu-id="f14a2-333">Bit</span></span> |
| <span data-ttu-id="f14a2-334">Decimal</span><span class="sxs-lookup"><span data-stu-id="f14a2-334">Decimal</span></span> | <span data-ttu-id="f14a2-335">Decimal</span><span class="sxs-lookup"><span data-stu-id="f14a2-335">Decimal</span></span> |
| <span data-ttu-id="f14a2-336">Numeric</span><span class="sxs-lookup"><span data-stu-id="f14a2-336">Numeric</span></span> | <span data-ttu-id="f14a2-337">Decimal</span><span class="sxs-lookup"><span data-stu-id="f14a2-337">Decimal</span></span> |
| <span data-ttu-id="f14a2-338">Float</span><span class="sxs-lookup"><span data-stu-id="f14a2-338">Float</span></span> | <span data-ttu-id="f14a2-339">Float</span><span class="sxs-lookup"><span data-stu-id="f14a2-339">Float</span></span> |
| <span data-ttu-id="f14a2-340">Money</span><span class="sxs-lookup"><span data-stu-id="f14a2-340">Money</span></span> | <span data-ttu-id="f14a2-341">Money</span><span class="sxs-lookup"><span data-stu-id="f14a2-341">Money</span></span> |
| <span data-ttu-id="f14a2-342">Real</span><span class="sxs-lookup"><span data-stu-id="f14a2-342">Real</span></span> | <span data-ttu-id="f14a2-343">Real</span><span class="sxs-lookup"><span data-stu-id="f14a2-343">Real</span></span> |
| <span data-ttu-id="f14a2-344">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="f14a2-344">SmallMoney</span></span> | <span data-ttu-id="f14a2-345">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="f14a2-345">SmallMoney</span></span> |
| <span data-ttu-id="f14a2-346">Binary</span><span class="sxs-lookup"><span data-stu-id="f14a2-346">Binary</span></span> | <span data-ttu-id="f14a2-347">Binary</span><span class="sxs-lookup"><span data-stu-id="f14a2-347">Binary</span></span> |
| <span data-ttu-id="f14a2-348">Varbinary</span><span class="sxs-lookup"><span data-stu-id="f14a2-348">Varbinary</span></span> | <span data-ttu-id="f14a2-349">Varbinary (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="f14a2-349">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="f14a2-350">Date</span><span class="sxs-lookup"><span data-stu-id="f14a2-350">Date</span></span> | <span data-ttu-id="f14a2-351">Date</span><span class="sxs-lookup"><span data-stu-id="f14a2-351">Date</span></span> |
| <span data-ttu-id="f14a2-352">DateTime</span><span class="sxs-lookup"><span data-stu-id="f14a2-352">DateTime</span></span> | <span data-ttu-id="f14a2-353">DateTime</span><span class="sxs-lookup"><span data-stu-id="f14a2-353">DateTime</span></span> |
| <span data-ttu-id="f14a2-354">DateTime2</span><span class="sxs-lookup"><span data-stu-id="f14a2-354">DateTime2</span></span> | <span data-ttu-id="f14a2-355">DateTime2</span><span class="sxs-lookup"><span data-stu-id="f14a2-355">DateTime2</span></span> |
| <span data-ttu-id="f14a2-356">Time</span><span class="sxs-lookup"><span data-stu-id="f14a2-356">Time</span></span> | <span data-ttu-id="f14a2-357">Time</span><span class="sxs-lookup"><span data-stu-id="f14a2-357">Time</span></span> |
| <span data-ttu-id="f14a2-358">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="f14a2-358">DateTimeOffset</span></span> | <span data-ttu-id="f14a2-359">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="f14a2-359">DateTimeOffset</span></span> |
| <span data-ttu-id="f14a2-360">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="f14a2-360">SmallDateTime</span></span> | <span data-ttu-id="f14a2-361">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="f14a2-361">SmallDateTime</span></span> |
| <span data-ttu-id="f14a2-362">Text</span><span class="sxs-lookup"><span data-stu-id="f14a2-362">Text</span></span> | <span data-ttu-id="f14a2-363">Varchar (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="f14a2-363">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="f14a2-364">NText</span><span class="sxs-lookup"><span data-stu-id="f14a2-364">NText</span></span> | <span data-ttu-id="f14a2-365">NVarChar (up to 4000)</span><span class="sxs-lookup"><span data-stu-id="f14a2-365">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="f14a2-366">Image</span><span class="sxs-lookup"><span data-stu-id="f14a2-366">Image</span></span> | <span data-ttu-id="f14a2-367">VarBinary (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="f14a2-367">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="f14a2-368">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="f14a2-368">UniqueIdentifier</span></span> | <span data-ttu-id="f14a2-369">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="f14a2-369">UniqueIdentifier</span></span> |
| <span data-ttu-id="f14a2-370">Char</span><span class="sxs-lookup"><span data-stu-id="f14a2-370">Char</span></span> | <span data-ttu-id="f14a2-371">Char</span><span class="sxs-lookup"><span data-stu-id="f14a2-371">Char</span></span> |
| <span data-ttu-id="f14a2-372">NChar</span><span class="sxs-lookup"><span data-stu-id="f14a2-372">NChar</span></span> | <span data-ttu-id="f14a2-373">NChar</span><span class="sxs-lookup"><span data-stu-id="f14a2-373">NChar</span></span> |
| <span data-ttu-id="f14a2-374">VarChar</span><span class="sxs-lookup"><span data-stu-id="f14a2-374">VarChar</span></span> | <span data-ttu-id="f14a2-375">VarChar (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="f14a2-375">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="f14a2-376">NVarChar</span><span class="sxs-lookup"><span data-stu-id="f14a2-376">NVarChar</span></span> | <span data-ttu-id="f14a2-377">NVarChar (up to 4000)</span><span class="sxs-lookup"><span data-stu-id="f14a2-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="f14a2-378">Xml</span><span class="sxs-lookup"><span data-stu-id="f14a2-378">Xml</span></span> | <span data-ttu-id="f14a2-379">Varchar (up to 8000)</span><span class="sxs-lookup"><span data-stu-id="f14a2-379">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

### <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="f14a2-380">Type mapping for Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f14a2-380">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f14a2-381">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="f14a2-381">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="f14a2-382">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="f14a2-382">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f14a2-383">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="f14a2-383">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f14a2-384">When moving data to & from Azure SQL, SQL server, Sybase the following mappings are used from SQL type to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="f14a2-384">When moving data to & from Azure SQL, SQL server, Sybase the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="f14a2-385">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="f14a2-385">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="f14a2-386">SQL Server Database Engine type</span><span class="sxs-lookup"><span data-stu-id="f14a2-386">SQL Server Database Engine type</span></span> | <span data-ttu-id="f14a2-387">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="f14a2-387">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="f14a2-388">bigint</span><span class="sxs-lookup"><span data-stu-id="f14a2-388">bigint</span></span> |<span data-ttu-id="f14a2-389">Int64</span><span class="sxs-lookup"><span data-stu-id="f14a2-389">Int64</span></span> |
| <span data-ttu-id="f14a2-390">binary</span><span class="sxs-lookup"><span data-stu-id="f14a2-390">binary</span></span> |<span data-ttu-id="f14a2-391">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-391">Byte[]</span></span> |
| <span data-ttu-id="f14a2-392">bit</span><span class="sxs-lookup"><span data-stu-id="f14a2-392">bit</span></span> |<span data-ttu-id="f14a2-393">Boolean</span><span class="sxs-lookup"><span data-stu-id="f14a2-393">Boolean</span></span> |
| <span data-ttu-id="f14a2-394">char</span><span class="sxs-lookup"><span data-stu-id="f14a2-394">char</span></span> |<span data-ttu-id="f14a2-395">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-395">String, Char[]</span></span> |
| <span data-ttu-id="f14a2-396">date</span><span class="sxs-lookup"><span data-stu-id="f14a2-396">date</span></span> |<span data-ttu-id="f14a2-397">DateTime</span><span class="sxs-lookup"><span data-stu-id="f14a2-397">DateTime</span></span> |
| <span data-ttu-id="f14a2-398">Datetime</span><span class="sxs-lookup"><span data-stu-id="f14a2-398">Datetime</span></span> |<span data-ttu-id="f14a2-399">DateTime</span><span class="sxs-lookup"><span data-stu-id="f14a2-399">DateTime</span></span> |
| <span data-ttu-id="f14a2-400">datetime2</span><span class="sxs-lookup"><span data-stu-id="f14a2-400">datetime2</span></span> |<span data-ttu-id="f14a2-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="f14a2-401">DateTime</span></span> |
| <span data-ttu-id="f14a2-402">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f14a2-402">Datetimeoffset</span></span> |<span data-ttu-id="f14a2-403">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="f14a2-403">DateTimeOffset</span></span> |
| <span data-ttu-id="f14a2-404">Decimal</span><span class="sxs-lookup"><span data-stu-id="f14a2-404">Decimal</span></span> |<span data-ttu-id="f14a2-405">Decimal</span><span class="sxs-lookup"><span data-stu-id="f14a2-405">Decimal</span></span> |
| <span data-ttu-id="f14a2-406">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="f14a2-406">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="f14a2-407">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-407">Byte[]</span></span> |
| <span data-ttu-id="f14a2-408">Float</span><span class="sxs-lookup"><span data-stu-id="f14a2-408">Float</span></span> |<span data-ttu-id="f14a2-409">Double</span><span class="sxs-lookup"><span data-stu-id="f14a2-409">Double</span></span> |
| <span data-ttu-id="f14a2-410">image</span><span class="sxs-lookup"><span data-stu-id="f14a2-410">image</span></span> |<span data-ttu-id="f14a2-411">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-411">Byte[]</span></span> |
| <span data-ttu-id="f14a2-412">int</span><span class="sxs-lookup"><span data-stu-id="f14a2-412">int</span></span> |<span data-ttu-id="f14a2-413">Int32</span><span class="sxs-lookup"><span data-stu-id="f14a2-413">Int32</span></span> |
| <span data-ttu-id="f14a2-414">money</span><span class="sxs-lookup"><span data-stu-id="f14a2-414">money</span></span> |<span data-ttu-id="f14a2-415">Decimal</span><span class="sxs-lookup"><span data-stu-id="f14a2-415">Decimal</span></span> |
| <span data-ttu-id="f14a2-416">nchar</span><span class="sxs-lookup"><span data-stu-id="f14a2-416">nchar</span></span> |<span data-ttu-id="f14a2-417">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-417">String, Char[]</span></span> |
| <span data-ttu-id="f14a2-418">ntext</span><span class="sxs-lookup"><span data-stu-id="f14a2-418">ntext</span></span> |<span data-ttu-id="f14a2-419">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-419">String, Char[]</span></span> |
| <span data-ttu-id="f14a2-420">numeric</span><span class="sxs-lookup"><span data-stu-id="f14a2-420">numeric</span></span> |<span data-ttu-id="f14a2-421">Decimal</span><span class="sxs-lookup"><span data-stu-id="f14a2-421">Decimal</span></span> |
| <span data-ttu-id="f14a2-422">nvarchar</span><span class="sxs-lookup"><span data-stu-id="f14a2-422">nvarchar</span></span> |<span data-ttu-id="f14a2-423">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-423">String, Char[]</span></span> |
| <span data-ttu-id="f14a2-424">real</span><span class="sxs-lookup"><span data-stu-id="f14a2-424">real</span></span> |<span data-ttu-id="f14a2-425">Single</span><span class="sxs-lookup"><span data-stu-id="f14a2-425">Single</span></span> |
| <span data-ttu-id="f14a2-426">rowversion</span><span class="sxs-lookup"><span data-stu-id="f14a2-426">rowversion</span></span> |<span data-ttu-id="f14a2-427">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-427">Byte[]</span></span> |
| <span data-ttu-id="f14a2-428">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="f14a2-428">smalldatetime</span></span> |<span data-ttu-id="f14a2-429">DateTime</span><span class="sxs-lookup"><span data-stu-id="f14a2-429">DateTime</span></span> |
| <span data-ttu-id="f14a2-430">smallint</span><span class="sxs-lookup"><span data-stu-id="f14a2-430">smallint</span></span> |<span data-ttu-id="f14a2-431">Int16</span><span class="sxs-lookup"><span data-stu-id="f14a2-431">Int16</span></span> |
| <span data-ttu-id="f14a2-432">smallmoney</span><span class="sxs-lookup"><span data-stu-id="f14a2-432">smallmoney</span></span> |<span data-ttu-id="f14a2-433">Decimal</span><span class="sxs-lookup"><span data-stu-id="f14a2-433">Decimal</span></span> |
| <span data-ttu-id="f14a2-434">sql_variant</span><span class="sxs-lookup"><span data-stu-id="f14a2-434">sql_variant</span></span> |<span data-ttu-id="f14a2-435">Object \*</span><span class="sxs-lookup"><span data-stu-id="f14a2-435">Object \*</span></span> |
| <span data-ttu-id="f14a2-436">text</span><span class="sxs-lookup"><span data-stu-id="f14a2-436">text</span></span> |<span data-ttu-id="f14a2-437">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-437">String, Char[]</span></span> |
| <span data-ttu-id="f14a2-438">time</span><span class="sxs-lookup"><span data-stu-id="f14a2-438">time</span></span> |<span data-ttu-id="f14a2-439">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f14a2-439">TimeSpan</span></span> |
| <span data-ttu-id="f14a2-440">timestamp</span><span class="sxs-lookup"><span data-stu-id="f14a2-440">timestamp</span></span> |<span data-ttu-id="f14a2-441">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-441">Byte[]</span></span> |
| <span data-ttu-id="f14a2-442">tinyint</span><span class="sxs-lookup"><span data-stu-id="f14a2-442">tinyint</span></span> |<span data-ttu-id="f14a2-443">Byte</span><span class="sxs-lookup"><span data-stu-id="f14a2-443">Byte</span></span> |
| <span data-ttu-id="f14a2-444">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="f14a2-444">uniqueidentifier</span></span> |<span data-ttu-id="f14a2-445">Guid</span><span class="sxs-lookup"><span data-stu-id="f14a2-445">Guid</span></span> |
| <span data-ttu-id="f14a2-446">varbinary</span><span class="sxs-lookup"><span data-stu-id="f14a2-446">varbinary</span></span> |<span data-ttu-id="f14a2-447">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-447">Byte[]</span></span> |
| <span data-ttu-id="f14a2-448">varchar</span><span class="sxs-lookup"><span data-stu-id="f14a2-448">varchar</span></span> |<span data-ttu-id="f14a2-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f14a2-449">String, Char[]</span></span> |
| <span data-ttu-id="f14a2-450">xml</span><span class="sxs-lookup"><span data-stu-id="f14a2-450">xml</span></span> |<span data-ttu-id="f14a2-451">Xml</span><span class="sxs-lookup"><span data-stu-id="f14a2-451">Xml</span></span> |

<span data-ttu-id="f14a2-452">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span><span class="sxs-lookup"><span data-stu-id="f14a2-452">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="f14a2-453">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f14a2-453">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples"></a><span data-ttu-id="f14a2-454">JSON examples</span><span class="sxs-lookup"><span data-stu-id="f14a2-454">JSON examples</span></span>
<span data-ttu-id="f14a2-455">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f14a2-455">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f14a2-456">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f14a2-456">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="f14a2-457">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f14a2-457">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="f14a2-458">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="f14a2-458">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="f14a2-459">The sample defines the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="f14a2-459">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="f14a2-460">A linked service of type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-460">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="f14a2-461">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-461">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f14a2-462">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-462">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="f14a2-463">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-463">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f14a2-464">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-464">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f14a2-465">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="f14a2-465">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="f14a2-466">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="f14a2-466">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f14a2-467">**Azure SQL Data Warehouse linked service:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-467">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="f14a2-468">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-468">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="f14a2-469">**Azure SQL Data Warehouse input dataset:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-469">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="f14a2-470">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="f14a2-470">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="f14a2-471">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f14a2-471">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="f14a2-472">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-472">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f14a2-473">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f14a2-473">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f14a2-474">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="f14a2-474">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f14a2-475">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="f14a2-475">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="f14a2-476">**Copy activity in a pipeline with SqlDWSource and BlobSink :**</span><span class="sxs-lookup"><span data-stu-id="f14a2-476">**Copy activity in a pipeline with SqlDWSource and BlobSink :**</span></span>

<span data-ttu-id="f14a2-477">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="f14a2-477">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f14a2-478">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f14a2-478">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f14a2-479">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="f14a2-479">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="f14a2-480">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="f14a2-480">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="f14a2-481">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span><span class="sxs-lookup"><span data-stu-id="f14a2-481">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="f14a2-482">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="f14a2-482">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="f14a2-483">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-483">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f14a2-484">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="f14a2-484">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

## <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="f14a2-485">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f14a2-485">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f14a2-486">The sample defines the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="f14a2-486">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="f14a2-487">A linked service of type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-487">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="f14a2-488">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-488">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f14a2-489">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-489">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="f14a2-490">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-490">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="f14a2-491">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f14a2-491">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="f14a2-492">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span><span class="sxs-lookup"><span data-stu-id="f14a2-492">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="f14a2-493">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="f14a2-493">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f14a2-494">**Azure SQL Data Warehouse linked service:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-494">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="f14a2-495">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-495">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="f14a2-496">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-496">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="f14a2-497">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f14a2-497">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f14a2-498">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="f14a2-498">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f14a2-499">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="f14a2-499">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="f14a2-500">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f14a2-500">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="f14a2-501">**Azure SQL Data Warehouse output dataset:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-501">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="f14a2-502">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f14a2-502">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f14a2-503">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="f14a2-503">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="f14a2-504">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="f14a2-504">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="f14a2-505">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="f14a2-505">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="f14a2-506">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="f14a2-506">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f14a2-507">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="f14a2-507">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

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
<span data-ttu-id="f14a2-508">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span><span class="sxs-lookup"><span data-stu-id="f14a2-508">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f14a2-509">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="f14a2-509">Performance and Tuning</span></span>
<span data-ttu-id="f14a2-510">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="f14a2-510">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
