---
title: Move data to/from Azure SQL Database | Microsoft Docs
description: Learn how to move data to/from Azure SQL Database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: jingwang
ms.openlocfilehash: c2616c6ff91a8fe78d60ed3bbae90b0739a6c104
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555056"
---
# <a name="move-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="32fb2-103">Move data to and from Azure SQL Database using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="32fb2-103">Move data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="32fb2-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="32fb2-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Database.</span></span> <span data-ttu-id="32fb2-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="32fb2-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

<span data-ttu-id="32fb2-106">You can copy data from any supported source data store to Azure SQL Database or from Azure SQL Database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="32fb2-106">You can copy data from any supported source data store to Azure SQL Database or from Azure SQL Database to any supported sink data store.</span></span> <span data-ttu-id="32fb2-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="32fb2-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="32fb2-108">Supported authentication type</span><span class="sxs-lookup"><span data-stu-id="32fb2-108">Supported authentication type</span></span>
<span data-ttu-id="32fb2-109">Azure SQL Database connector support basic authentication.</span><span class="sxs-lookup"><span data-stu-id="32fb2-109">Azure SQL Database connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="32fb2-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="32fb2-110">Getting started</span></span>
<span data-ttu-id="32fb2-111">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="32fb2-111">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="32fb2-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="32fb2-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="32fb2-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="32fb2-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="32fb2-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="32fb2-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="32fb2-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="32fb2-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="32fb2-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="32fb2-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="32fb2-117">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="32fb2-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="32fb2-118">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="32fb2-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="32fb2-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="32fb2-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="32fb2-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="32fb2-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="32fb2-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="32fb2-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="32fb2-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="32fb2-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="32fb2-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="32fb2-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="32fb2-124">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="32fb2-124">Linked service properties</span></span>
<span data-ttu-id="32fb2-125">An Azure SQL linked service links an Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="32fb2-125">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="32fb2-126">The following table provides description for JSON elements specific to Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="32fb2-126">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="32fb2-127">Property</span><span class="sxs-lookup"><span data-stu-id="32fb2-127">Property</span></span> | <span data-ttu-id="32fb2-128">Description</span><span class="sxs-lookup"><span data-stu-id="32fb2-128">Description</span></span> | <span data-ttu-id="32fb2-129">Required</span><span class="sxs-lookup"><span data-stu-id="32fb2-129">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32fb2-130">type</span><span class="sxs-lookup"><span data-stu-id="32fb2-130">type</span></span> |<span data-ttu-id="32fb2-131">The type property must be set to: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="32fb2-131">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="32fb2-132">Yes</span><span class="sxs-lookup"><span data-stu-id="32fb2-132">Yes</span></span> |
| <span data-ttu-id="32fb2-133">connectionString</span><span class="sxs-lookup"><span data-stu-id="32fb2-133">connectionString</span></span> |<span data-ttu-id="32fb2-134">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="32fb2-134">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="32fb2-135">Only basic authentication is supported.</span><span class="sxs-lookup"><span data-stu-id="32fb2-135">Only basic authentication is supported.</span></span> |<span data-ttu-id="32fb2-136">Yes</span><span class="sxs-lookup"><span data-stu-id="32fb2-136">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="32fb2-137">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="32fb2-137">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="32fb2-138">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="32fb2-138">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="32fb2-139">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="32fb2-139">Dataset properties</span></span>
<span data-ttu-id="32fb2-140">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="32fb2-140">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="32fb2-141">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="32fb2-141">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="32fb2-142">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="32fb2-142">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="32fb2-143">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="32fb2-143">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="32fb2-144">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="32fb2-144">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="32fb2-145">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="32fb2-145">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="32fb2-146">Property</span><span class="sxs-lookup"><span data-stu-id="32fb2-146">Property</span></span> | <span data-ttu-id="32fb2-147">Description</span><span class="sxs-lookup"><span data-stu-id="32fb2-147">Description</span></span> | <span data-ttu-id="32fb2-148">Required</span><span class="sxs-lookup"><span data-stu-id="32fb2-148">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32fb2-149">tableName</span><span class="sxs-lookup"><span data-stu-id="32fb2-149">tableName</span></span> |<span data-ttu-id="32fb2-150">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="32fb2-150">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="32fb2-151">Yes</span><span class="sxs-lookup"><span data-stu-id="32fb2-151">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="32fb2-152">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="32fb2-152">Copy activity properties</span></span>
<span data-ttu-id="32fb2-153">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="32fb2-153">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="32fb2-154">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="32fb2-154">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="32fb2-155">The Copy Activity takes only one input and produces only one output.</span><span class="sxs-lookup"><span data-stu-id="32fb2-155">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="32fb2-156">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="32fb2-156">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="32fb2-157">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="32fb2-157">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="32fb2-158">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="32fb2-158">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="32fb2-159">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="32fb2-159">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="32fb2-160">This section provides a list of properties supported by SqlSource and SqlSink.</span><span class="sxs-lookup"><span data-stu-id="32fb2-160">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="32fb2-161">SqlSource</span><span class="sxs-lookup"><span data-stu-id="32fb2-161">SqlSource</span></span>
<span data-ttu-id="32fb2-162">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="32fb2-162">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="32fb2-163">Property</span><span class="sxs-lookup"><span data-stu-id="32fb2-163">Property</span></span> | <span data-ttu-id="32fb2-164">Description</span><span class="sxs-lookup"><span data-stu-id="32fb2-164">Description</span></span> | <span data-ttu-id="32fb2-165">Allowed values</span><span class="sxs-lookup"><span data-stu-id="32fb2-165">Allowed values</span></span> | <span data-ttu-id="32fb2-166">Required</span><span class="sxs-lookup"><span data-stu-id="32fb2-166">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="32fb2-167">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="32fb2-167">sqlReaderQuery</span></span> |<span data-ttu-id="32fb2-168">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="32fb2-168">Use the custom query to read data.</span></span> |<span data-ttu-id="32fb2-169">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="32fb2-169">SQL query string.</span></span> <span data-ttu-id="32fb2-170">Example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="32fb2-170">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="32fb2-171">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-171">No</span></span> |
| <span data-ttu-id="32fb2-172">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="32fb2-172">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="32fb2-173">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="32fb2-173">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="32fb2-174">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="32fb2-174">Name of the stored procedure.</span></span> <span data-ttu-id="32fb2-175">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="32fb2-175">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="32fb2-176">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-176">No</span></span> |
| <span data-ttu-id="32fb2-177">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="32fb2-177">storedProcedureParameters</span></span> |<span data-ttu-id="32fb2-178">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="32fb2-178">Parameters for the stored procedure.</span></span> |<span data-ttu-id="32fb2-179">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="32fb2-179">Name/value pairs.</span></span> <span data-ttu-id="32fb2-180">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="32fb2-180">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="32fb2-181">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-181">No</span></span> |

<span data-ttu-id="32fb2-182">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="32fb2-182">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="32fb2-183">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="32fb2-183">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="32fb2-184">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="32fb2-184">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="32fb2-185">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="32fb2-185">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="32fb2-186">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span><span class="sxs-lookup"><span data-stu-id="32fb2-186">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="32fb2-187">There are no validations performed against this table though.</span><span class="sxs-lookup"><span data-stu-id="32fb2-187">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="32fb2-188">SqlSource example</span><span class="sxs-lookup"><span data-stu-id="32fb2-188">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="32fb2-189">**The stored procedure definition:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-189">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="32fb2-190">SqlSink</span><span class="sxs-lookup"><span data-stu-id="32fb2-190">SqlSink</span></span>
<span data-ttu-id="32fb2-191">**SqlSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="32fb2-191">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="32fb2-192">Property</span><span class="sxs-lookup"><span data-stu-id="32fb2-192">Property</span></span> | <span data-ttu-id="32fb2-193">Description</span><span class="sxs-lookup"><span data-stu-id="32fb2-193">Description</span></span> | <span data-ttu-id="32fb2-194">Allowed values</span><span class="sxs-lookup"><span data-stu-id="32fb2-194">Allowed values</span></span> | <span data-ttu-id="32fb2-195">Required</span><span class="sxs-lookup"><span data-stu-id="32fb2-195">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="32fb2-196">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="32fb2-196">writeBatchTimeout</span></span> |<span data-ttu-id="32fb2-197">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="32fb2-197">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="32fb2-198">timespan</span><span class="sxs-lookup"><span data-stu-id="32fb2-198">timespan</span></span><br/><br/> <span data-ttu-id="32fb2-199">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="32fb2-199">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="32fb2-200">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-200">No</span></span> |
| <span data-ttu-id="32fb2-201">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="32fb2-201">writeBatchSize</span></span> |<span data-ttu-id="32fb2-202">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="32fb2-202">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="32fb2-203">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="32fb2-203">Integer (number of rows)</span></span> |<span data-ttu-id="32fb2-204">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="32fb2-204">No (default: 10000)</span></span> |
| <span data-ttu-id="32fb2-205">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="32fb2-205">sqlWriterCleanupScript</span></span> |<span data-ttu-id="32fb2-206">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="32fb2-206">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="32fb2-207">For more information, see [repeatability section](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="32fb2-207">For more information, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="32fb2-208">A query statement.</span><span class="sxs-lookup"><span data-stu-id="32fb2-208">A query statement.</span></span> |<span data-ttu-id="32fb2-209">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-209">No</span></span> |
| <span data-ttu-id="32fb2-210">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="32fb2-210">sliceIdentifierColumnName</span></span> |<span data-ttu-id="32fb2-211">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="32fb2-211">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="32fb2-212">For more information, see [repeatability section](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="32fb2-212">For more information, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="32fb2-213">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="32fb2-213">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="32fb2-214">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-214">No</span></span> |
| <span data-ttu-id="32fb2-215">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="32fb2-215">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="32fb2-216">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span><span class="sxs-lookup"><span data-stu-id="32fb2-216">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="32fb2-217">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="32fb2-217">Name of the stored procedure.</span></span> |<span data-ttu-id="32fb2-218">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-218">No</span></span> |
| <span data-ttu-id="32fb2-219">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="32fb2-219">storedProcedureParameters</span></span> |<span data-ttu-id="32fb2-220">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="32fb2-220">Parameters for the stored procedure.</span></span> |<span data-ttu-id="32fb2-221">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="32fb2-221">Name/value pairs.</span></span> <span data-ttu-id="32fb2-222">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="32fb2-222">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="32fb2-223">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-223">No</span></span> |
| <span data-ttu-id="32fb2-224">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="32fb2-224">sqlWriterTableType</span></span> |<span data-ttu-id="32fb2-225">Specify a table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="32fb2-225">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="32fb2-226">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="32fb2-226">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="32fb2-227">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="32fb2-227">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="32fb2-228">A table type name.</span><span class="sxs-lookup"><span data-stu-id="32fb2-228">A table type name.</span></span> |<span data-ttu-id="32fb2-229">No</span><span class="sxs-lookup"><span data-stu-id="32fb2-229">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="32fb2-230">SqlSink example</span><span class="sxs-lookup"><span data-stu-id="32fb2-230">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples"></a><span data-ttu-id="32fb2-231">JSON examples</span><span class="sxs-lookup"><span data-stu-id="32fb2-231">JSON examples</span></span>
<span data-ttu-id="32fb2-232">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="32fb2-232">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="32fb2-233">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="32fb2-233">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="32fb2-234">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="32fb2-234">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="32fb2-235">Example: Copy data from Azure SQL Database to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="32fb2-235">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="32fb2-236">The same defines the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="32fb2-236">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="32fb2-237">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-237">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="32fb2-238">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-238">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="32fb2-239">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-239">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="32fb2-240">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-240">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="32fb2-241">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-241">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="32fb2-242">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="32fb2-242">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="32fb2-243">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="32fb2-243">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="32fb2-244">**Azure SQL Database linked service:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-244">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="32fb2-245">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="32fb2-245">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="32fb2-246">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-246">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="32fb2-247">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="32fb2-247">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="32fb2-248">**Azure SQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-248">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="32fb2-249">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="32fb2-249">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="32fb2-250">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="32fb2-250">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="32fb2-251">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span><span class="sxs-lookup"><span data-stu-id="32fb2-251">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="32fb2-252">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-252">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="32fb2-253">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="32fb2-253">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="32fb2-254">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="32fb2-254">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="32fb2-255">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="32fb2-255">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
<span data-ttu-id="32fb2-256">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span><span class="sxs-lookup"><span data-stu-id="32fb2-256">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="32fb2-257">**A copy activity in a pipeline with SQL source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-257">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="32fb2-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="32fb2-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="32fb2-259">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="32fb2-259">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="32fb2-260">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="32fb2-260">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="32fb2-261">In the example, **sqlReaderQuery** is specified for the SqlSource.</span><span class="sxs-lookup"><span data-stu-id="32fb2-261">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="32fb2-262">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="32fb2-262">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="32fb2-263">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="32fb2-263">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="32fb2-264">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="32fb2-264">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="32fb2-265">For example: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="32fb2-265">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="32fb2-266">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="32fb2-266">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="32fb2-267">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span><span class="sxs-lookup"><span data-stu-id="32fb2-267">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="32fb2-268">Example: Copy data from Azure Blob to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="32fb2-268">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="32fb2-269">The sample defines the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="32fb2-269">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="32fb2-270">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-270">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="32fb2-271">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-271">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="32fb2-272">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-272">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="32fb2-273">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-273">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="32fb2-274">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="32fb2-274">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="32fb2-275">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span><span class="sxs-lookup"><span data-stu-id="32fb2-275">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="32fb2-276">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="32fb2-276">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="32fb2-277">**Azure SQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-277">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="32fb2-278">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="32fb2-278">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="32fb2-279">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-279">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="32fb2-280">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="32fb2-280">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="32fb2-281">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-281">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="32fb2-282">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="32fb2-282">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="32fb2-283">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="32fb2-283">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="32fb2-284">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="32fb2-284">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="32fb2-285">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="32fb2-285">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="32fb2-286">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span><span class="sxs-lookup"><span data-stu-id="32fb2-286">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="32fb2-287">**Azure SQL Database output dataset:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-287">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="32fb2-288">The sample copies data to a table named “MyTable” in Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="32fb2-288">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="32fb2-289">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="32fb2-289">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="32fb2-290">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="32fb2-290">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
<span data-ttu-id="32fb2-291">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span><span class="sxs-lookup"><span data-stu-id="32fb2-291">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="32fb2-292">**A copy activity in a pipeline with Blob source and SQL sink:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-292">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="32fb2-293">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="32fb2-293">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="32fb2-294">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="32fb2-294">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
<span data-ttu-id="32fb2-295">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span><span class="sxs-lookup"><span data-stu-id="32fb2-295">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="32fb2-296">Identity columns in the target database</span><span class="sxs-lookup"><span data-stu-id="32fb2-296">Identity columns in the target database</span></span>
<span data-ttu-id="32fb2-297">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span><span class="sxs-lookup"><span data-stu-id="32fb2-297">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="32fb2-298">**Source table:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-298">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="32fb2-299">**Destination table:**</span><span class="sxs-lookup"><span data-stu-id="32fb2-299">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="32fb2-300">Notice that the target table has an identity column.</span><span class="sxs-lookup"><span data-stu-id="32fb2-300">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="32fb2-301">**Source dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="32fb2-301">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="32fb2-302">**Destination dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="32fb2-302">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="32fb2-303">Notice that as your source and target table have different schema (target has an additional column with identity).</span><span class="sxs-lookup"><span data-stu-id="32fb2-303">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="32fb2-304">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span><span class="sxs-lookup"><span data-stu-id="32fb2-304">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="32fb2-305">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="32fb2-305">Map source to sink columns</span></span>
<span data-ttu-id="32fb2-306">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="32fb2-306">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="32fb2-307">Repeatable copy</span><span class="sxs-lookup"><span data-stu-id="32fb2-307">Repeatable copy</span></span>
<span data-ttu-id="32fb2-308">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span><span class="sxs-lookup"><span data-stu-id="32fb2-308">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="32fb2-309">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span><span class="sxs-lookup"><span data-stu-id="32fb2-309">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="32fb2-310">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="32fb2-310">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="32fb2-311">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="32fb2-311">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="32fb2-312">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="32fb2-312">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="32fb2-313">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="32fb2-313">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="32fb2-314">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="32fb2-314">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="32fb2-315">Invoke stored procedure from SQL sink</span><span class="sxs-lookup"><span data-stu-id="32fb2-315">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="32fb2-316">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="32fb2-316">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="sql-database-to-net-type-mapping"></a><span data-ttu-id="32fb2-317">SQL Database to .NET type mapping</span><span class="sxs-lookup"><span data-stu-id="32fb2-317">SQL Database to .NET type mapping</span></span>
<span data-ttu-id="32fb2-318">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="32fb2-318">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="32fb2-319">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="32fb2-319">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="32fb2-320">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="32fb2-320">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="32fb2-321">When moving data to and from Azure SQL, the following mappings are used from SQL type to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="32fb2-321">When moving data to and from Azure SQL, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="32fb2-322">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="32fb2-322">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="32fb2-323">SQL Server Database Engine type</span><span class="sxs-lookup"><span data-stu-id="32fb2-323">SQL Server Database Engine type</span></span> | <span data-ttu-id="32fb2-324">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="32fb2-324">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="32fb2-325">bigint</span><span class="sxs-lookup"><span data-stu-id="32fb2-325">bigint</span></span> |<span data-ttu-id="32fb2-326">Int64</span><span class="sxs-lookup"><span data-stu-id="32fb2-326">Int64</span></span> |
| <span data-ttu-id="32fb2-327">binary</span><span class="sxs-lookup"><span data-stu-id="32fb2-327">binary</span></span> |<span data-ttu-id="32fb2-328">Byte[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-328">Byte[]</span></span> |
| <span data-ttu-id="32fb2-329">bit</span><span class="sxs-lookup"><span data-stu-id="32fb2-329">bit</span></span> |<span data-ttu-id="32fb2-330">Boolean</span><span class="sxs-lookup"><span data-stu-id="32fb2-330">Boolean</span></span> |
| <span data-ttu-id="32fb2-331">char</span><span class="sxs-lookup"><span data-stu-id="32fb2-331">char</span></span> |<span data-ttu-id="32fb2-332">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-332">String, Char[]</span></span> |
| <span data-ttu-id="32fb2-333">date</span><span class="sxs-lookup"><span data-stu-id="32fb2-333">date</span></span> |<span data-ttu-id="32fb2-334">DateTime</span><span class="sxs-lookup"><span data-stu-id="32fb2-334">DateTime</span></span> |
| <span data-ttu-id="32fb2-335">Datetime</span><span class="sxs-lookup"><span data-stu-id="32fb2-335">Datetime</span></span> |<span data-ttu-id="32fb2-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="32fb2-336">DateTime</span></span> |
| <span data-ttu-id="32fb2-337">datetime2</span><span class="sxs-lookup"><span data-stu-id="32fb2-337">datetime2</span></span> |<span data-ttu-id="32fb2-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="32fb2-338">DateTime</span></span> |
| <span data-ttu-id="32fb2-339">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="32fb2-339">Datetimeoffset</span></span> |<span data-ttu-id="32fb2-340">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="32fb2-340">DateTimeOffset</span></span> |
| <span data-ttu-id="32fb2-341">Decimal</span><span class="sxs-lookup"><span data-stu-id="32fb2-341">Decimal</span></span> |<span data-ttu-id="32fb2-342">Decimal</span><span class="sxs-lookup"><span data-stu-id="32fb2-342">Decimal</span></span> |
| <span data-ttu-id="32fb2-343">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="32fb2-343">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="32fb2-344">Byte[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-344">Byte[]</span></span> |
| <span data-ttu-id="32fb2-345">Float</span><span class="sxs-lookup"><span data-stu-id="32fb2-345">Float</span></span> |<span data-ttu-id="32fb2-346">Double</span><span class="sxs-lookup"><span data-stu-id="32fb2-346">Double</span></span> |
| <span data-ttu-id="32fb2-347">image</span><span class="sxs-lookup"><span data-stu-id="32fb2-347">image</span></span> |<span data-ttu-id="32fb2-348">Byte[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-348">Byte[]</span></span> |
| <span data-ttu-id="32fb2-349">int</span><span class="sxs-lookup"><span data-stu-id="32fb2-349">int</span></span> |<span data-ttu-id="32fb2-350">Int32</span><span class="sxs-lookup"><span data-stu-id="32fb2-350">Int32</span></span> |
| <span data-ttu-id="32fb2-351">money</span><span class="sxs-lookup"><span data-stu-id="32fb2-351">money</span></span> |<span data-ttu-id="32fb2-352">Decimal</span><span class="sxs-lookup"><span data-stu-id="32fb2-352">Decimal</span></span> |
| <span data-ttu-id="32fb2-353">nchar</span><span class="sxs-lookup"><span data-stu-id="32fb2-353">nchar</span></span> |<span data-ttu-id="32fb2-354">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-354">String, Char[]</span></span> |
| <span data-ttu-id="32fb2-355">ntext</span><span class="sxs-lookup"><span data-stu-id="32fb2-355">ntext</span></span> |<span data-ttu-id="32fb2-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-356">String, Char[]</span></span> |
| <span data-ttu-id="32fb2-357">numeric</span><span class="sxs-lookup"><span data-stu-id="32fb2-357">numeric</span></span> |<span data-ttu-id="32fb2-358">Decimal</span><span class="sxs-lookup"><span data-stu-id="32fb2-358">Decimal</span></span> |
| <span data-ttu-id="32fb2-359">nvarchar</span><span class="sxs-lookup"><span data-stu-id="32fb2-359">nvarchar</span></span> |<span data-ttu-id="32fb2-360">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-360">String, Char[]</span></span> |
| <span data-ttu-id="32fb2-361">real</span><span class="sxs-lookup"><span data-stu-id="32fb2-361">real</span></span> |<span data-ttu-id="32fb2-362">Single</span><span class="sxs-lookup"><span data-stu-id="32fb2-362">Single</span></span> |
| <span data-ttu-id="32fb2-363">rowversion</span><span class="sxs-lookup"><span data-stu-id="32fb2-363">rowversion</span></span> |<span data-ttu-id="32fb2-364">Byte[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-364">Byte[]</span></span> |
| <span data-ttu-id="32fb2-365">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="32fb2-365">smalldatetime</span></span> |<span data-ttu-id="32fb2-366">DateTime</span><span class="sxs-lookup"><span data-stu-id="32fb2-366">DateTime</span></span> |
| <span data-ttu-id="32fb2-367">smallint</span><span class="sxs-lookup"><span data-stu-id="32fb2-367">smallint</span></span> |<span data-ttu-id="32fb2-368">Int16</span><span class="sxs-lookup"><span data-stu-id="32fb2-368">Int16</span></span> |
| <span data-ttu-id="32fb2-369">smallmoney</span><span class="sxs-lookup"><span data-stu-id="32fb2-369">smallmoney</span></span> |<span data-ttu-id="32fb2-370">Decimal</span><span class="sxs-lookup"><span data-stu-id="32fb2-370">Decimal</span></span> |
| <span data-ttu-id="32fb2-371">sql_variant</span><span class="sxs-lookup"><span data-stu-id="32fb2-371">sql_variant</span></span> |<span data-ttu-id="32fb2-372">Object \*</span><span class="sxs-lookup"><span data-stu-id="32fb2-372">Object \*</span></span> |
| <span data-ttu-id="32fb2-373">text</span><span class="sxs-lookup"><span data-stu-id="32fb2-373">text</span></span> |<span data-ttu-id="32fb2-374">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-374">String, Char[]</span></span> |
| <span data-ttu-id="32fb2-375">time</span><span class="sxs-lookup"><span data-stu-id="32fb2-375">time</span></span> |<span data-ttu-id="32fb2-376">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="32fb2-376">TimeSpan</span></span> |
| <span data-ttu-id="32fb2-377">timestamp</span><span class="sxs-lookup"><span data-stu-id="32fb2-377">timestamp</span></span> |<span data-ttu-id="32fb2-378">Byte[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-378">Byte[]</span></span> |
| <span data-ttu-id="32fb2-379">tinyint</span><span class="sxs-lookup"><span data-stu-id="32fb2-379">tinyint</span></span> |<span data-ttu-id="32fb2-380">Byte</span><span class="sxs-lookup"><span data-stu-id="32fb2-380">Byte</span></span> |
| <span data-ttu-id="32fb2-381">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="32fb2-381">uniqueidentifier</span></span> |<span data-ttu-id="32fb2-382">Guid</span><span class="sxs-lookup"><span data-stu-id="32fb2-382">Guid</span></span> |
| <span data-ttu-id="32fb2-383">varbinary</span><span class="sxs-lookup"><span data-stu-id="32fb2-383">varbinary</span></span> |<span data-ttu-id="32fb2-384">Byte[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-384">Byte[]</span></span> |
| <span data-ttu-id="32fb2-385">varchar</span><span class="sxs-lookup"><span data-stu-id="32fb2-385">varchar</span></span> |<span data-ttu-id="32fb2-386">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="32fb2-386">String, Char[]</span></span> |
| <span data-ttu-id="32fb2-387">xml</span><span class="sxs-lookup"><span data-stu-id="32fb2-387">xml</span></span> |<span data-ttu-id="32fb2-388">Xml</span><span class="sxs-lookup"><span data-stu-id="32fb2-388">Xml</span></span> |

## <a name="performance-and-tuning"></a><span data-ttu-id="32fb2-389">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="32fb2-389">Performance and Tuning</span></span>
<span data-ttu-id="32fb2-390">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="32fb2-390">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
