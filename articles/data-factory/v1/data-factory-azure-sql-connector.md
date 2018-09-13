---
title: Copy data to/from Azure SQL Database | Microsoft Docs
description: Learn how to copy data to/from Azure SQL Database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: d010fd90d96409b262be59f1db4fac9e4cec835c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868172"
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="a4d77-103">Copy data to and from Azure SQL Database using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a4d77-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-azure-sql-connector.md)
> * [Version 2 (current version)](../connector-azure-sql-database.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Azure SQL Database connector in V2](../connector-azure-sql-database.md).

<span data-ttu-id="a4d77-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4d77-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="a4d77-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="a4d77-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="a4d77-110">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="a4d77-110">Supported scenarios</span></span>
<span data-ttu-id="a4d77-111">You can copy data **from Azure SQL Database** to the following data stores:</span><span class="sxs-lookup"><span data-stu-id="a4d77-111">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="a4d77-112">You can copy data from the following data stores **to Azure SQL Database**:</span><span class="sxs-lookup"><span data-stu-id="a4d77-112">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="a4d77-113">Supported authentication type</span><span class="sxs-lookup"><span data-stu-id="a4d77-113">Supported authentication type</span></span>
<span data-ttu-id="a4d77-114">Azure SQL Database connector supports basic authentication.</span><span class="sxs-lookup"><span data-stu-id="a4d77-114">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a4d77-115">Getting started</span><span class="sxs-lookup"><span data-stu-id="a4d77-115">Getting started</span></span>
<span data-ttu-id="a4d77-116">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="a4d77-116">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="a4d77-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a4d77-118">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="a4d77-118">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="a4d77-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a4d77-120">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="a4d77-120">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a4d77-121">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="a4d77-121">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="a4d77-122">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-122">Create a **data factory**.</span></span> <span data-ttu-id="a4d77-123">A data factory may contain one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="a4d77-123">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="a4d77-124">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="a4d77-124">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="a4d77-125">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="a4d77-125">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="a4d77-126">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="a4d77-126">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="a4d77-127">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="a4d77-127">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="a4d77-128">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="a4d77-128">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="a4d77-129">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span><span class="sxs-lookup"><span data-stu-id="a4d77-129">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="a4d77-130">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="a4d77-130">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="a4d77-131">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="a4d77-131">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="a4d77-132">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="a4d77-132">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="a4d77-133">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span><span class="sxs-lookup"><span data-stu-id="a4d77-133">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="a4d77-134">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="a4d77-134">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="a4d77-135">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span><span class="sxs-lookup"><span data-stu-id="a4d77-135">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="a4d77-136">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="a4d77-136">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a4d77-137">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="a4d77-137">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a4d77-138">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span><span class="sxs-lookup"><span data-stu-id="a4d77-138">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="a4d77-139">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="a4d77-139">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="a4d77-140">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="a4d77-140">Linked service properties</span></span>
<span data-ttu-id="a4d77-141">An Azure SQL linked service links an Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="a4d77-141">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="a4d77-142">The following table provides description for JSON elements specific to Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="a4d77-142">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="a4d77-143">Property</span><span class="sxs-lookup"><span data-stu-id="a4d77-143">Property</span></span> | <span data-ttu-id="a4d77-144">Description</span><span class="sxs-lookup"><span data-stu-id="a4d77-144">Description</span></span> | <span data-ttu-id="a4d77-145">Required</span><span class="sxs-lookup"><span data-stu-id="a4d77-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4d77-146">type</span><span class="sxs-lookup"><span data-stu-id="a4d77-146">type</span></span> |<span data-ttu-id="a4d77-147">The type property must be set to: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="a4d77-147">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="a4d77-148">Yes</span><span class="sxs-lookup"><span data-stu-id="a4d77-148">Yes</span></span> |
| <span data-ttu-id="a4d77-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="a4d77-149">connectionString</span></span> |<span data-ttu-id="a4d77-150">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="a4d77-150">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="a4d77-151">Only basic authentication is supported.</span><span class="sxs-lookup"><span data-stu-id="a4d77-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="a4d77-152">Yes</span><span class="sxs-lookup"><span data-stu-id="a4d77-152">Yes</span></span> |

> [!IMPORTANT]
> Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.

## <a name="dataset-properties"></a><span data-ttu-id="a4d77-155">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="a4d77-155">Dataset properties</span></span>
<span data-ttu-id="a4d77-156">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-156">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="a4d77-157">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="a4d77-157">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="a4d77-158">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="a4d77-158">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a4d77-159">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="a4d77-159">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a4d77-160">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="a4d77-160">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a4d77-161">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="a4d77-161">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="a4d77-162">Property</span><span class="sxs-lookup"><span data-stu-id="a4d77-162">Property</span></span> | <span data-ttu-id="a4d77-163">Description</span><span class="sxs-lookup"><span data-stu-id="a4d77-163">Description</span></span> | <span data-ttu-id="a4d77-164">Required</span><span class="sxs-lookup"><span data-stu-id="a4d77-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4d77-165">tableName</span><span class="sxs-lookup"><span data-stu-id="a4d77-165">tableName</span></span> |<span data-ttu-id="a4d77-166">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="a4d77-166">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="a4d77-167">Yes</span><span class="sxs-lookup"><span data-stu-id="a4d77-167">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a4d77-168">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="a4d77-168">Copy activity properties</span></span>
<span data-ttu-id="a4d77-169">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="a4d77-169">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a4d77-170">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="a4d77-170">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> The Copy Activity takes only one input and produces only one output.

<span data-ttu-id="a4d77-172">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="a4d77-172">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="a4d77-173">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="a4d77-173">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a4d77-174">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-174">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="a4d77-175">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-175">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="a4d77-176">This section provides a list of properties supported by SqlSource and SqlSink.</span><span class="sxs-lookup"><span data-stu-id="a4d77-176">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="a4d77-177">SqlSource</span><span class="sxs-lookup"><span data-stu-id="a4d77-177">SqlSource</span></span>
<span data-ttu-id="a4d77-178">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="a4d77-178">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="a4d77-179">Property</span><span class="sxs-lookup"><span data-stu-id="a4d77-179">Property</span></span> | <span data-ttu-id="a4d77-180">Description</span><span class="sxs-lookup"><span data-stu-id="a4d77-180">Description</span></span> | <span data-ttu-id="a4d77-181">Allowed values</span><span class="sxs-lookup"><span data-stu-id="a4d77-181">Allowed values</span></span> | <span data-ttu-id="a4d77-182">Required</span><span class="sxs-lookup"><span data-stu-id="a4d77-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a4d77-183">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="a4d77-183">sqlReaderQuery</span></span> |<span data-ttu-id="a4d77-184">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="a4d77-184">Use the custom query to read data.</span></span> |<span data-ttu-id="a4d77-185">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="a4d77-185">SQL query string.</span></span> <span data-ttu-id="a4d77-186">Example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="a4d77-186">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="a4d77-187">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-187">No</span></span> |
| <span data-ttu-id="a4d77-188">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="a4d77-188">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="a4d77-189">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="a4d77-189">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="a4d77-190">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a4d77-190">Name of the stored procedure.</span></span> <span data-ttu-id="a4d77-191">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a4d77-191">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="a4d77-192">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-192">No</span></span> |
| <span data-ttu-id="a4d77-193">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="a4d77-193">storedProcedureParameters</span></span> |<span data-ttu-id="a4d77-194">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a4d77-194">Parameters for the stored procedure.</span></span> |<span data-ttu-id="a4d77-195">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="a4d77-195">Name/value pairs.</span></span> <span data-ttu-id="a4d77-196">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="a4d77-196">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="a4d77-197">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-197">No</span></span> |

<span data-ttu-id="a4d77-198">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="a4d77-198">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="a4d77-199">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="a4d77-199">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="a4d77-200">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4d77-200">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="a4d77-201">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="a4d77-201">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON. There are no validations performed against this table though.
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="a4d77-204">SqlSource example</span><span class="sxs-lookup"><span data-stu-id="a4d77-204">SqlSource example</span></span>

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

<span data-ttu-id="a4d77-205">**The stored procedure definition:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-205">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="a4d77-206">SqlSink</span><span class="sxs-lookup"><span data-stu-id="a4d77-206">SqlSink</span></span>
<span data-ttu-id="a4d77-207">**SqlSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="a4d77-207">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="a4d77-208">Property</span><span class="sxs-lookup"><span data-stu-id="a4d77-208">Property</span></span> | <span data-ttu-id="a4d77-209">Description</span><span class="sxs-lookup"><span data-stu-id="a4d77-209">Description</span></span> | <span data-ttu-id="a4d77-210">Allowed values</span><span class="sxs-lookup"><span data-stu-id="a4d77-210">Allowed values</span></span> | <span data-ttu-id="a4d77-211">Required</span><span class="sxs-lookup"><span data-stu-id="a4d77-211">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a4d77-212">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="a4d77-212">writeBatchTimeout</span></span> |<span data-ttu-id="a4d77-213">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="a4d77-213">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="a4d77-214">timespan</span><span class="sxs-lookup"><span data-stu-id="a4d77-214">timespan</span></span><br/><br/> <span data-ttu-id="a4d77-215">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="a4d77-215">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="a4d77-216">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-216">No</span></span> |
| <span data-ttu-id="a4d77-217">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="a4d77-217">writeBatchSize</span></span> |<span data-ttu-id="a4d77-218">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="a4d77-218">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="a4d77-219">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="a4d77-219">Integer (number of rows)</span></span> |<span data-ttu-id="a4d77-220">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="a4d77-220">No (default: 10000)</span></span> |
| <span data-ttu-id="a4d77-221">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="a4d77-221">sqlWriterCleanupScript</span></span> |<span data-ttu-id="a4d77-222">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="a4d77-222">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="a4d77-223">For more information, see [repeatable copy](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="a4d77-223">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="a4d77-224">A query statement.</span><span class="sxs-lookup"><span data-stu-id="a4d77-224">A query statement.</span></span> |<span data-ttu-id="a4d77-225">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-225">No</span></span> |
| <span data-ttu-id="a4d77-226">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="a4d77-226">sliceIdentifierColumnName</span></span> |<span data-ttu-id="a4d77-227">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="a4d77-227">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="a4d77-228">For more information, see [repeatable copy](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="a4d77-228">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="a4d77-229">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="a4d77-229">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="a4d77-230">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-230">No</span></span> |
| <span data-ttu-id="a4d77-231">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="a4d77-231">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="a4d77-232">Name of the stored procedure that defines how to apply source data into target table, e.g. to do upserts or transform using your own business logic.</span><span class="sxs-lookup"><span data-stu-id="a4d77-232">Name of the stored procedure that defines how to apply source data into target table, e.g. to do upserts or transform using your own business logic.</span></span> <br/><br/><span data-ttu-id="a4d77-233">Note this stored procedure will be **invoked per batch**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-233">Note this stored procedure will be **invoked per batch**.</span></span> <span data-ttu-id="a4d77-234">If you want to do operation that only runs once and has nothing to do with source data e.g. delete/truncate, use `sqlWriterCleanupScript` property.</span><span class="sxs-lookup"><span data-stu-id="a4d77-234">If you want to do operation that only runs once and has nothing to do with source data e.g. delete/truncate, use `sqlWriterCleanupScript` property.</span></span> |<span data-ttu-id="a4d77-235">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a4d77-235">Name of the stored procedure.</span></span> |<span data-ttu-id="a4d77-236">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-236">No</span></span> |
| <span data-ttu-id="a4d77-237">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="a4d77-237">storedProcedureParameters</span></span> |<span data-ttu-id="a4d77-238">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a4d77-238">Parameters for the stored procedure.</span></span> |<span data-ttu-id="a4d77-239">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="a4d77-239">Name/value pairs.</span></span> <span data-ttu-id="a4d77-240">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="a4d77-240">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="a4d77-241">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-241">No</span></span> |
| <span data-ttu-id="a4d77-242">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="a4d77-242">sqlWriterTableType</span></span> |<span data-ttu-id="a4d77-243">Specify a table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a4d77-243">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="a4d77-244">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="a4d77-244">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="a4d77-245">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="a4d77-245">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="a4d77-246">A table type name.</span><span class="sxs-lookup"><span data-stu-id="a4d77-246">A table type name.</span></span> |<span data-ttu-id="a4d77-247">No</span><span class="sxs-lookup"><span data-stu-id="a4d77-247">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="a4d77-248">SqlSink example</span><span class="sxs-lookup"><span data-stu-id="a4d77-248">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="a4d77-249">JSON examples for copying data to and from SQL Database</span><span class="sxs-lookup"><span data-stu-id="a4d77-249">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="a4d77-250">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a4d77-250">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a4d77-251">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a4d77-251">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="a4d77-252">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a4d77-252">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="a4d77-253">Example: Copy data from Azure SQL Database to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a4d77-253">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="a4d77-254">The same defines the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="a4d77-254">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="a4d77-255">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-255">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="a4d77-256">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-256">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a4d77-257">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-257">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a4d77-258">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-258">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a4d77-259">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-259">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a4d77-260">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="a4d77-260">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="a4d77-261">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="a4d77-261">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="a4d77-262">**Azure SQL Database linked service:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-262">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="a4d77-263">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="a4d77-263">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="a4d77-264">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-264">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="a4d77-265">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="a4d77-265">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="a4d77-266">**Azure SQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-266">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="a4d77-267">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="a4d77-267">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="a4d77-268">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="a4d77-268">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="a4d77-269">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span><span class="sxs-lookup"><span data-stu-id="a4d77-269">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="a4d77-270">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-270">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a4d77-271">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a4d77-271">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a4d77-272">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="a4d77-272">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a4d77-273">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="a4d77-273">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="a4d77-274">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span><span class="sxs-lookup"><span data-stu-id="a4d77-274">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="a4d77-275">**A copy activity in a pipeline with SQL source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-275">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="a4d77-276">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="a4d77-276">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a4d77-277">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-277">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="a4d77-278">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="a4d77-278">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="a4d77-279">In the example, **sqlReaderQuery** is specified for the SqlSource.</span><span class="sxs-lookup"><span data-stu-id="a4d77-279">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="a4d77-280">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="a4d77-280">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="a4d77-281">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="a4d77-281">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="a4d77-282">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4d77-282">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="a4d77-283">For example: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="a4d77-283">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="a4d77-284">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="a4d77-284">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="a4d77-285">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span><span class="sxs-lookup"><span data-stu-id="a4d77-285">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="a4d77-286">Example: Copy data from Azure Blob to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a4d77-286">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="a4d77-287">The sample defines the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="a4d77-287">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="a4d77-288">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-288">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="a4d77-289">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-289">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a4d77-290">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-290">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="a4d77-291">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-291">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="a4d77-292">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a4d77-292">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="a4d77-293">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span><span class="sxs-lookup"><span data-stu-id="a4d77-293">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="a4d77-294">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="a4d77-294">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a4d77-295">**Azure SQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-295">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="a4d77-296">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="a4d77-296">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="a4d77-297">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-297">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="a4d77-298">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="a4d77-298">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="a4d77-299">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-299">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="a4d77-300">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a4d77-300">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a4d77-301">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="a4d77-301">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a4d77-302">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="a4d77-302">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="a4d77-303">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="a4d77-303">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="a4d77-304">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span><span class="sxs-lookup"><span data-stu-id="a4d77-304">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="a4d77-305">**Azure SQL Database output dataset:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-305">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="a4d77-306">The sample copies data to a table named “MyTable” in Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="a4d77-306">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="a4d77-307">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="a4d77-307">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="a4d77-308">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="a4d77-308">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="a4d77-309">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span><span class="sxs-lookup"><span data-stu-id="a4d77-309">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="a4d77-310">**A copy activity in a pipeline with Blob source and SQL sink:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-310">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="a4d77-311">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="a4d77-311">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a4d77-312">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="a4d77-312">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
<span data-ttu-id="a4d77-313">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span><span class="sxs-lookup"><span data-stu-id="a4d77-313">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="a4d77-314">Identity columns in the target database</span><span class="sxs-lookup"><span data-stu-id="a4d77-314">Identity columns in the target database</span></span>
<span data-ttu-id="a4d77-315">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span><span class="sxs-lookup"><span data-stu-id="a4d77-315">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="a4d77-316">**Source table:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-316">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="a4d77-317">**Destination table:**</span><span class="sxs-lookup"><span data-stu-id="a4d77-317">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="a4d77-318">Notice that the target table has an identity column.</span><span class="sxs-lookup"><span data-stu-id="a4d77-318">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="a4d77-319">**Source dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="a4d77-319">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="a4d77-320">**Destination dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="a4d77-320">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="a4d77-321">Notice that as your source and target table have different schema (target has an additional column with identity).</span><span class="sxs-lookup"><span data-stu-id="a4d77-321">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="a4d77-322">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span><span class="sxs-lookup"><span data-stu-id="a4d77-322">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="a4d77-323">Invoke stored procedure from SQL sink</span><span class="sxs-lookup"><span data-stu-id="a4d77-323">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="a4d77-324">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="a4d77-324">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="a4d77-325">Type mapping for Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a4d77-325">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="a4d77-326">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="a4d77-326">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="a4d77-327">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="a4d77-327">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="a4d77-328">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="a4d77-328">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="a4d77-329">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="a4d77-329">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="a4d77-330">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="a4d77-330">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="a4d77-331">SQL Server Database Engine type</span><span class="sxs-lookup"><span data-stu-id="a4d77-331">SQL Server Database Engine type</span></span> | <span data-ttu-id="a4d77-332">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="a4d77-332">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="a4d77-333">bigint</span><span class="sxs-lookup"><span data-stu-id="a4d77-333">bigint</span></span> |<span data-ttu-id="a4d77-334">Int64</span><span class="sxs-lookup"><span data-stu-id="a4d77-334">Int64</span></span> |
| <span data-ttu-id="a4d77-335">binary</span><span class="sxs-lookup"><span data-stu-id="a4d77-335">binary</span></span> |<span data-ttu-id="a4d77-336">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-336">Byte[]</span></span> |
| <span data-ttu-id="a4d77-337">bit</span><span class="sxs-lookup"><span data-stu-id="a4d77-337">bit</span></span> |<span data-ttu-id="a4d77-338">Boolean</span><span class="sxs-lookup"><span data-stu-id="a4d77-338">Boolean</span></span> |
| <span data-ttu-id="a4d77-339">char</span><span class="sxs-lookup"><span data-stu-id="a4d77-339">char</span></span> |<span data-ttu-id="a4d77-340">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-340">String, Char[]</span></span> |
| <span data-ttu-id="a4d77-341">date</span><span class="sxs-lookup"><span data-stu-id="a4d77-341">date</span></span> |<span data-ttu-id="a4d77-342">DateTime</span><span class="sxs-lookup"><span data-stu-id="a4d77-342">DateTime</span></span> |
| <span data-ttu-id="a4d77-343">Datetime</span><span class="sxs-lookup"><span data-stu-id="a4d77-343">Datetime</span></span> |<span data-ttu-id="a4d77-344">DateTime</span><span class="sxs-lookup"><span data-stu-id="a4d77-344">DateTime</span></span> |
| <span data-ttu-id="a4d77-345">datetime2</span><span class="sxs-lookup"><span data-stu-id="a4d77-345">datetime2</span></span> |<span data-ttu-id="a4d77-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="a4d77-346">DateTime</span></span> |
| <span data-ttu-id="a4d77-347">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a4d77-347">Datetimeoffset</span></span> |<span data-ttu-id="a4d77-348">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a4d77-348">DateTimeOffset</span></span> |
| <span data-ttu-id="a4d77-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="a4d77-349">Decimal</span></span> |<span data-ttu-id="a4d77-350">Decimal</span><span class="sxs-lookup"><span data-stu-id="a4d77-350">Decimal</span></span> |
| <span data-ttu-id="a4d77-351">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="a4d77-351">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="a4d77-352">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-352">Byte[]</span></span> |
| <span data-ttu-id="a4d77-353">Float</span><span class="sxs-lookup"><span data-stu-id="a4d77-353">Float</span></span> |<span data-ttu-id="a4d77-354">Double</span><span class="sxs-lookup"><span data-stu-id="a4d77-354">Double</span></span> |
| <span data-ttu-id="a4d77-355">image</span><span class="sxs-lookup"><span data-stu-id="a4d77-355">image</span></span> |<span data-ttu-id="a4d77-356">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-356">Byte[]</span></span> |
| <span data-ttu-id="a4d77-357">int</span><span class="sxs-lookup"><span data-stu-id="a4d77-357">int</span></span> |<span data-ttu-id="a4d77-358">Int32</span><span class="sxs-lookup"><span data-stu-id="a4d77-358">Int32</span></span> |
| <span data-ttu-id="a4d77-359">money</span><span class="sxs-lookup"><span data-stu-id="a4d77-359">money</span></span> |<span data-ttu-id="a4d77-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="a4d77-360">Decimal</span></span> |
| <span data-ttu-id="a4d77-361">nchar</span><span class="sxs-lookup"><span data-stu-id="a4d77-361">nchar</span></span> |<span data-ttu-id="a4d77-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-362">String, Char[]</span></span> |
| <span data-ttu-id="a4d77-363">ntext</span><span class="sxs-lookup"><span data-stu-id="a4d77-363">ntext</span></span> |<span data-ttu-id="a4d77-364">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-364">String, Char[]</span></span> |
| <span data-ttu-id="a4d77-365">numeric</span><span class="sxs-lookup"><span data-stu-id="a4d77-365">numeric</span></span> |<span data-ttu-id="a4d77-366">Decimal</span><span class="sxs-lookup"><span data-stu-id="a4d77-366">Decimal</span></span> |
| <span data-ttu-id="a4d77-367">nvarchar</span><span class="sxs-lookup"><span data-stu-id="a4d77-367">nvarchar</span></span> |<span data-ttu-id="a4d77-368">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-368">String, Char[]</span></span> |
| <span data-ttu-id="a4d77-369">real</span><span class="sxs-lookup"><span data-stu-id="a4d77-369">real</span></span> |<span data-ttu-id="a4d77-370">Single</span><span class="sxs-lookup"><span data-stu-id="a4d77-370">Single</span></span> |
| <span data-ttu-id="a4d77-371">rowversion</span><span class="sxs-lookup"><span data-stu-id="a4d77-371">rowversion</span></span> |<span data-ttu-id="a4d77-372">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-372">Byte[]</span></span> |
| <span data-ttu-id="a4d77-373">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="a4d77-373">smalldatetime</span></span> |<span data-ttu-id="a4d77-374">DateTime</span><span class="sxs-lookup"><span data-stu-id="a4d77-374">DateTime</span></span> |
| <span data-ttu-id="a4d77-375">smallint</span><span class="sxs-lookup"><span data-stu-id="a4d77-375">smallint</span></span> |<span data-ttu-id="a4d77-376">Int16</span><span class="sxs-lookup"><span data-stu-id="a4d77-376">Int16</span></span> |
| <span data-ttu-id="a4d77-377">smallmoney</span><span class="sxs-lookup"><span data-stu-id="a4d77-377">smallmoney</span></span> |<span data-ttu-id="a4d77-378">Decimal</span><span class="sxs-lookup"><span data-stu-id="a4d77-378">Decimal</span></span> |
| <span data-ttu-id="a4d77-379">sql_variant</span><span class="sxs-lookup"><span data-stu-id="a4d77-379">sql_variant</span></span> |<span data-ttu-id="a4d77-380">Object \*</span><span class="sxs-lookup"><span data-stu-id="a4d77-380">Object \*</span></span> |
| <span data-ttu-id="a4d77-381">text</span><span class="sxs-lookup"><span data-stu-id="a4d77-381">text</span></span> |<span data-ttu-id="a4d77-382">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-382">String, Char[]</span></span> |
| <span data-ttu-id="a4d77-383">time</span><span class="sxs-lookup"><span data-stu-id="a4d77-383">time</span></span> |<span data-ttu-id="a4d77-384">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a4d77-384">TimeSpan</span></span> |
| <span data-ttu-id="a4d77-385">timestamp</span><span class="sxs-lookup"><span data-stu-id="a4d77-385">timestamp</span></span> |<span data-ttu-id="a4d77-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-386">Byte[]</span></span> |
| <span data-ttu-id="a4d77-387">tinyint</span><span class="sxs-lookup"><span data-stu-id="a4d77-387">tinyint</span></span> |<span data-ttu-id="a4d77-388">Byte</span><span class="sxs-lookup"><span data-stu-id="a4d77-388">Byte</span></span> |
| <span data-ttu-id="a4d77-389">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="a4d77-389">uniqueidentifier</span></span> |<span data-ttu-id="a4d77-390">Guid</span><span class="sxs-lookup"><span data-stu-id="a4d77-390">Guid</span></span> |
| <span data-ttu-id="a4d77-391">varbinary</span><span class="sxs-lookup"><span data-stu-id="a4d77-391">varbinary</span></span> |<span data-ttu-id="a4d77-392">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-392">Byte[]</span></span> |
| <span data-ttu-id="a4d77-393">varchar</span><span class="sxs-lookup"><span data-stu-id="a4d77-393">varchar</span></span> |<span data-ttu-id="a4d77-394">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a4d77-394">String, Char[]</span></span> |
| <span data-ttu-id="a4d77-395">xml</span><span class="sxs-lookup"><span data-stu-id="a4d77-395">xml</span></span> |<span data-ttu-id="a4d77-396">Xml</span><span class="sxs-lookup"><span data-stu-id="a4d77-396">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="a4d77-397">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="a4d77-397">Map source to sink columns</span></span>
<span data-ttu-id="a4d77-398">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a4d77-398">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="a4d77-399">Repeatable copy</span><span class="sxs-lookup"><span data-stu-id="a4d77-399">Repeatable copy</span></span>
<span data-ttu-id="a4d77-400">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span><span class="sxs-lookup"><span data-stu-id="a4d77-400">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="a4d77-401">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span><span class="sxs-lookup"><span data-stu-id="a4d77-401">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="a4d77-402">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="a4d77-402">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="a4d77-403">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="a4d77-403">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a4d77-404">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="a4d77-404">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a4d77-405">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="a4d77-405">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a4d77-406">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="a4d77-406">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a4d77-407">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="a4d77-407">Performance and Tuning</span></span>
<span data-ttu-id="a4d77-408">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="a4d77-408">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
