---
title: Move data to/from DocumentDB | Microsoft Docs
description: Learn how move data to/from Azure DocumentDB collection using Azure Data Factory
services: data-factory, documentdb
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jingwang
ms.openlocfilehash: d5e13e6a96828e7c303e4d870ee170b90a0c4308
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564497"
---
# <a name="move-data-to-and-from-documentdb-using-azure-data-factory"></a><span data-ttu-id="43fcd-103">Move data to and from DocumentDB using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="43fcd-103">Move data to and from DocumentDB using Azure Data Factory</span></span>
<span data-ttu-id="43fcd-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="43fcd-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure DocumentDB.</span></span> <span data-ttu-id="43fcd-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="43fcd-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="43fcd-106">You can copy data from any supported source data store to Azure DocumentDB or from Azure DocumentDB to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="43fcd-106">You can copy data from any supported source data store to Azure DocumentDB or from Azure DocumentDB to any supported sink data store.</span></span> <span data-ttu-id="43fcd-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="43fcd-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!NOTE]
> <span data-ttu-id="43fcd-108">Copying data from on-premises/Azure IaaS data stores to Azure DocumentDB and vice versa are supported with Data Management Gateway version 2.1 and above.</span><span class="sxs-lookup"><span data-stu-id="43fcd-108">Copying data from on-premises/Azure IaaS data stores to Azure DocumentDB and vice versa are supported with Data Management Gateway version 2.1 and above.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="43fcd-109">Supported versions</span><span class="sxs-lookup"><span data-stu-id="43fcd-109">Supported versions</span></span>
<span data-ttu-id="43fcd-110">This DocumentDB connector supports copying data from/to DocumentDB single partition collection and partitioned collection.</span><span class="sxs-lookup"><span data-stu-id="43fcd-110">This DocumentDB connector supports copying data from/to DocumentDB single partition collection and partitioned collection.</span></span> <span data-ttu-id="43fcd-111">[DocDB for MongoDB](../documentdb/documentdb-protocol-mongodb.md) is not supported.</span><span class="sxs-lookup"><span data-stu-id="43fcd-111">[DocDB for MongoDB](../documentdb/documentdb-protocol-mongodb.md) is not supported.</span></span> <span data-ttu-id="43fcd-112">To copy data as-is to/from JSON files or another DocumentDB collection, see [Import/Export JSON documents](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="43fcd-112">To copy data as-is to/from JSON files or another DocumentDB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="43fcd-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="43fcd-113">Getting started</span></span>
<span data-ttu-id="43fcd-114">You can create a pipeline with a copy activity that moves data to/from Azure DocumentDB by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="43fcd-114">You can create a pipeline with a copy activity that moves data to/from Azure DocumentDB by using different tools/APIs.</span></span>

<span data-ttu-id="43fcd-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="43fcd-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="43fcd-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="43fcd-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="43fcd-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="43fcd-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="43fcd-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="43fcd-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="43fcd-119">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="43fcd-119">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="43fcd-120">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="43fcd-120">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="43fcd-121">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="43fcd-121">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="43fcd-122">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="43fcd-122">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="43fcd-123">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="43fcd-123">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="43fcd-124">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="43fcd-124">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="43fcd-125">For samples with JSON definitions for Data Factory entities that are used to copy data to/from DocumentDB, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="43fcd-125">For samples with JSON definitions for Data Factory entities that are used to copy data to/from DocumentDB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="43fcd-126">The following sections provide details about JSON properties that are used to define Data Factory entities specific to DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="43fcd-126">The following sections provide details about JSON properties that are used to define Data Factory entities specific to DocumentDB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="43fcd-127">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="43fcd-127">Linked service properties</span></span>
<span data-ttu-id="43fcd-128">The following table provides description for JSON elements specific to Azure DocumentDB linked service.</span><span class="sxs-lookup"><span data-stu-id="43fcd-128">The following table provides description for JSON elements specific to Azure DocumentDB linked service.</span></span>

| <span data-ttu-id="43fcd-129">**Property**</span><span class="sxs-lookup"><span data-stu-id="43fcd-129">**Property**</span></span> | <span data-ttu-id="43fcd-130">**Description**</span><span class="sxs-lookup"><span data-stu-id="43fcd-130">**Description**</span></span> | <span data-ttu-id="43fcd-131">**Required**</span><span class="sxs-lookup"><span data-stu-id="43fcd-131">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43fcd-132">type</span><span class="sxs-lookup"><span data-stu-id="43fcd-132">type</span></span> |<span data-ttu-id="43fcd-133">The type property must be set to: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="43fcd-133">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="43fcd-134">Yes</span><span class="sxs-lookup"><span data-stu-id="43fcd-134">Yes</span></span> |
| <span data-ttu-id="43fcd-135">connectionString</span><span class="sxs-lookup"><span data-stu-id="43fcd-135">connectionString</span></span> |<span data-ttu-id="43fcd-136">Specify information needed to connect to Azure DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="43fcd-136">Specify information needed to connect to Azure DocumentDB database.</span></span> |<span data-ttu-id="43fcd-137">Yes</span><span class="sxs-lookup"><span data-stu-id="43fcd-137">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="43fcd-138">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="43fcd-138">Dataset properties</span></span>
<span data-ttu-id="43fcd-139">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="43fcd-139">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="43fcd-140">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="43fcd-140">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="43fcd-141">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="43fcd-141">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="43fcd-142">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span><span class="sxs-lookup"><span data-stu-id="43fcd-142">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="43fcd-143">**Property**</span><span class="sxs-lookup"><span data-stu-id="43fcd-143">**Property**</span></span> | <span data-ttu-id="43fcd-144">**Description**</span><span class="sxs-lookup"><span data-stu-id="43fcd-144">**Description**</span></span> | <span data-ttu-id="43fcd-145">**Required**</span><span class="sxs-lookup"><span data-stu-id="43fcd-145">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43fcd-146">collectionName</span><span class="sxs-lookup"><span data-stu-id="43fcd-146">collectionName</span></span> |<span data-ttu-id="43fcd-147">Name of the DocumentDB document collection.</span><span class="sxs-lookup"><span data-stu-id="43fcd-147">Name of the DocumentDB document collection.</span></span> |<span data-ttu-id="43fcd-148">Yes</span><span class="sxs-lookup"><span data-stu-id="43fcd-148">Yes</span></span> |

<span data-ttu-id="43fcd-149">Example:</span><span class="sxs-lookup"><span data-stu-id="43fcd-149">Example:</span></span>

```JSON
{
  "name": "PersonDocumentDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "DocumentDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="43fcd-150">Schema by Data Factory</span><span class="sxs-lookup"><span data-stu-id="43fcd-150">Schema by Data Factory</span></span>
<span data-ttu-id="43fcd-151">For schema-free data stores such as DocumentDB, the Data Factory service infers the schema in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="43fcd-151">For schema-free data stores such as DocumentDB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="43fcd-152">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span><span class="sxs-lookup"><span data-stu-id="43fcd-152">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="43fcd-153">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span><span class="sxs-lookup"><span data-stu-id="43fcd-153">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="43fcd-154">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span><span class="sxs-lookup"><span data-stu-id="43fcd-154">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="43fcd-155">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span><span class="sxs-lookup"><span data-stu-id="43fcd-155">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="43fcd-156">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span><span class="sxs-lookup"><span data-stu-id="43fcd-156">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="43fcd-157">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="43fcd-157">Copy activity properties</span></span>
<span data-ttu-id="43fcd-158">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="43fcd-158">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="43fcd-159">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="43fcd-159">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="43fcd-160">The Copy Activity takes only one input and produces only one output.</span><span class="sxs-lookup"><span data-stu-id="43fcd-160">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="43fcd-161">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="43fcd-161">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="43fcd-162">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="43fcd-162">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="43fcd-163">**Property**</span><span class="sxs-lookup"><span data-stu-id="43fcd-163">**Property**</span></span> | <span data-ttu-id="43fcd-164">**Description**</span><span class="sxs-lookup"><span data-stu-id="43fcd-164">**Description**</span></span> | <span data-ttu-id="43fcd-165">**Allowed values**</span><span class="sxs-lookup"><span data-stu-id="43fcd-165">**Allowed values**</span></span> | <span data-ttu-id="43fcd-166">**Required**</span><span class="sxs-lookup"><span data-stu-id="43fcd-166">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="43fcd-167">query</span><span class="sxs-lookup"><span data-stu-id="43fcd-167">query</span></span> |<span data-ttu-id="43fcd-168">Specify the query to read data.</span><span class="sxs-lookup"><span data-stu-id="43fcd-168">Specify the query to read data.</span></span> |<span data-ttu-id="43fcd-169">Query string supported by DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="43fcd-169">Query string supported by DocumentDB.</span></span> <br/><br/><span data-ttu-id="43fcd-170">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="43fcd-170">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="43fcd-171">No</span><span class="sxs-lookup"><span data-stu-id="43fcd-171">No</span></span> <br/><br/><span data-ttu-id="43fcd-172">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="43fcd-172">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="43fcd-173">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="43fcd-173">nestingSeparator</span></span> |<span data-ttu-id="43fcd-174">Special character to indicate that the document is nested</span><span class="sxs-lookup"><span data-stu-id="43fcd-174">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="43fcd-175">Any character.</span><span class="sxs-lookup"><span data-stu-id="43fcd-175">Any character.</span></span> <br/><br/><span data-ttu-id="43fcd-176">DocumentDB is a NoSQL store for JSON documents, where nested structures are allowed.</span><span class="sxs-lookup"><span data-stu-id="43fcd-176">DocumentDB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="43fcd-177">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span><span class="sxs-lookup"><span data-stu-id="43fcd-177">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="43fcd-178">in the above examples.</span><span class="sxs-lookup"><span data-stu-id="43fcd-178">in the above examples.</span></span> <span data-ttu-id="43fcd-179">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span><span class="sxs-lookup"><span data-stu-id="43fcd-179">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="43fcd-180">No</span><span class="sxs-lookup"><span data-stu-id="43fcd-180">No</span></span> |

<span data-ttu-id="43fcd-181">**DocumentDbCollectionSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="43fcd-181">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="43fcd-182">**Property**</span><span class="sxs-lookup"><span data-stu-id="43fcd-182">**Property**</span></span> | <span data-ttu-id="43fcd-183">**Description**</span><span class="sxs-lookup"><span data-stu-id="43fcd-183">**Description**</span></span> | <span data-ttu-id="43fcd-184">**Allowed values**</span><span class="sxs-lookup"><span data-stu-id="43fcd-184">**Allowed values**</span></span> | <span data-ttu-id="43fcd-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="43fcd-185">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="43fcd-186">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="43fcd-186">nestingSeparator</span></span> |<span data-ttu-id="43fcd-187">A special character in the source column name to indicate that nested document is needed.</span><span class="sxs-lookup"><span data-stu-id="43fcd-187">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="43fcd-188">For example above: `Name.First` in the output table produces the following JSON structure in the DocumentDB document:</span><span class="sxs-lookup"><span data-stu-id="43fcd-188">For example above: `Name.First` in the output table produces the following JSON structure in the DocumentDB document:</span></span><br/><br/><span data-ttu-id="43fcd-189">"Name": {</span><span class="sxs-lookup"><span data-stu-id="43fcd-189">"Name": {</span></span><br/>    <span data-ttu-id="43fcd-190">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="43fcd-190">"First": "John"</span></span><br/><span data-ttu-id="43fcd-191">},</span><span class="sxs-lookup"><span data-stu-id="43fcd-191">},</span></span> |<span data-ttu-id="43fcd-192">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="43fcd-192">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="43fcd-193">Default value is `.` (dot).</span><span class="sxs-lookup"><span data-stu-id="43fcd-193">Default value is `.` (dot).</span></span> |<span data-ttu-id="43fcd-194">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="43fcd-194">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="43fcd-195">Default value is `.` (dot).</span><span class="sxs-lookup"><span data-stu-id="43fcd-195">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="43fcd-196">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="43fcd-196">writeBatchSize</span></span> |<span data-ttu-id="43fcd-197">Number of parallel requests to DocumentDB service to create documents.</span><span class="sxs-lookup"><span data-stu-id="43fcd-197">Number of parallel requests to DocumentDB service to create documents.</span></span><br/><br/><span data-ttu-id="43fcd-198">You can fine-tune the performance when copying data to/from DocumentDB by using this property.</span><span class="sxs-lookup"><span data-stu-id="43fcd-198">You can fine-tune the performance when copying data to/from DocumentDB by using this property.</span></span> <span data-ttu-id="43fcd-199">You can expect a better performance when you increase writeBatchSize because more parallel requests to DocumentDB are sent.</span><span class="sxs-lookup"><span data-stu-id="43fcd-199">You can expect a better performance when you increase writeBatchSize because more parallel requests to DocumentDB are sent.</span></span> <span data-ttu-id="43fcd-200">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span><span class="sxs-lookup"><span data-stu-id="43fcd-200">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="43fcd-201">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span><span class="sxs-lookup"><span data-stu-id="43fcd-201">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="43fcd-202">Integer</span><span class="sxs-lookup"><span data-stu-id="43fcd-202">Integer</span></span> |<span data-ttu-id="43fcd-203">No (default: 5)</span><span class="sxs-lookup"><span data-stu-id="43fcd-203">No (default: 5)</span></span> |
| <span data-ttu-id="43fcd-204">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="43fcd-204">writeBatchTimeout</span></span> |<span data-ttu-id="43fcd-205">Wait time for the operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="43fcd-205">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="43fcd-206">timespan</span><span class="sxs-lookup"><span data-stu-id="43fcd-206">timespan</span></span><br/><br/> <span data-ttu-id="43fcd-207">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="43fcd-207">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="43fcd-208">No</span><span class="sxs-lookup"><span data-stu-id="43fcd-208">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="43fcd-209">Import/Export JSON documents</span><span class="sxs-lookup"><span data-stu-id="43fcd-209">Import/Export JSON documents</span></span>
<span data-ttu-id="43fcd-210">Using this DocumentDB connector, you can easily</span><span class="sxs-lookup"><span data-stu-id="43fcd-210">Using this DocumentDB connector, you can easily</span></span>

* <span data-ttu-id="43fcd-211">Import JSON documents from various sources into DocumentDB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="43fcd-211">Import JSON documents from various sources into DocumentDB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="43fcd-212">Export JSON documents from DocumentDB collecton into various file-based stores.</span><span class="sxs-lookup"><span data-stu-id="43fcd-212">Export JSON documents from DocumentDB collecton into various file-based stores.</span></span>
* <span data-ttu-id="43fcd-213">Migrate data between two DocumentDB collections as-is.</span><span class="sxs-lookup"><span data-stu-id="43fcd-213">Migrate data between two DocumentDB collections as-is.</span></span>

<span data-ttu-id="43fcd-214">To achieve such schema-agnostic copy,</span><span class="sxs-lookup"><span data-stu-id="43fcd-214">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="43fcd-215">When using copy wizard, check the **"Export as-is to JSON files or DocumentDB collection"** option.</span><span class="sxs-lookup"><span data-stu-id="43fcd-215">When using copy wizard, check the **"Export as-is to JSON files or DocumentDB collection"** option.</span></span>
* <span data-ttu-id="43fcd-216">When using JSON editing, do not specify the "structure" section in DocumentDB dataset(s) nor "nestingSeparator" property on DocumentDB source/sink in copy activity.</span><span class="sxs-lookup"><span data-stu-id="43fcd-216">When using JSON editing, do not specify the "structure" section in DocumentDB dataset(s) nor "nestingSeparator" property on DocumentDB source/sink in copy activity.</span></span> <span data-ttu-id="43fcd-217">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span><span class="sxs-lookup"><span data-stu-id="43fcd-217">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="43fcd-218">JSON examples</span><span class="sxs-lookup"><span data-stu-id="43fcd-218">JSON examples</span></span>
<span data-ttu-id="43fcd-219">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="43fcd-219">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="43fcd-220">They show how to copy data to and from Azure DocumentDB and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="43fcd-220">They show how to copy data to and from Azure DocumentDB and Azure Blob Storage.</span></span> <span data-ttu-id="43fcd-221">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="43fcd-221">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-documentdb-to-azure-blob"></a><span data-ttu-id="43fcd-222">Example: Copy data from DocumentDB to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="43fcd-222">Example: Copy data from DocumentDB to Azure Blob</span></span>
<span data-ttu-id="43fcd-223">The sample below shows:</span><span class="sxs-lookup"><span data-stu-id="43fcd-223">The sample below shows:</span></span>

1. <span data-ttu-id="43fcd-224">A linked service of type [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-224">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="43fcd-225">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-225">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="43fcd-226">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-226">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="43fcd-227">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-227">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="43fcd-228">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-228">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="43fcd-229">The sample copies data in Azure DocumentDB to Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="43fcd-229">The sample copies data in Azure DocumentDB to Azure Blob.</span></span> <span data-ttu-id="43fcd-230">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="43fcd-230">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="43fcd-231">**Azure DocumentDB linked service:**</span><span class="sxs-lookup"><span data-stu-id="43fcd-231">**Azure DocumentDB linked service:**</span></span>

```JSON
{
  "name": "DocumentDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="43fcd-232">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="43fcd-232">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="43fcd-233">**Azure Document DB input dataset:**</span><span class="sxs-lookup"><span data-stu-id="43fcd-233">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="43fcd-234">The sample assumes you have a collection named **Person** in an Azure DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="43fcd-234">The sample assumes you have a collection named **Person** in an Azure DocumentDB database.</span></span>

<span data-ttu-id="43fcd-235">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="43fcd-235">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "PersonDocumentDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "DocumentDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="43fcd-236">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="43fcd-236">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="43fcd-237">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span><span class="sxs-lookup"><span data-stu-id="43fcd-237">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="43fcd-238">Sample JSON document in the Person collection in a DocumentDB database:</span><span class="sxs-lookup"><span data-stu-id="43fcd-238">Sample JSON document in the Person collection in a DocumentDB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="43fcd-239">DocumentDB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span><span class="sxs-lookup"><span data-stu-id="43fcd-239">DocumentDB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="43fcd-240">Example:</span><span class="sxs-lookup"><span data-stu-id="43fcd-240">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="43fcd-241">The following pipeline copies data from the Person collection in the DocumentDB database to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="43fcd-241">The following pipeline copies data from the Person collection in the DocumentDB database to an Azure blob.</span></span> <span data-ttu-id="43fcd-242">As part of the copy activity the input and output datasets have been specified.</span><span class="sxs-lookup"><span data-stu-id="43fcd-242">As part of the copy activity the input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonDocumentDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-to-azure-documentdb"></a><span data-ttu-id="43fcd-243">Example: Copy data from Azure Blob to Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="43fcd-243">Example: Copy data from Azure Blob to Azure DocumentDB</span></span>
<span data-ttu-id="43fcd-244">The sample below shows:</span><span class="sxs-lookup"><span data-stu-id="43fcd-244">The sample below shows:</span></span>

1. <span data-ttu-id="43fcd-245">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-245">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="43fcd-246">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-246">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="43fcd-247">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-247">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="43fcd-248">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-248">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="43fcd-249">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="43fcd-249">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="43fcd-250">The sample copies data from Azure blob to Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="43fcd-250">The sample copies data from Azure blob to Azure DocumentDB.</span></span> <span data-ttu-id="43fcd-251">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="43fcd-251">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="43fcd-252">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="43fcd-252">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="43fcd-253">**Azure DocumentDB linked service:**</span><span class="sxs-lookup"><span data-stu-id="43fcd-253">**Azure DocumentDB linked service:**</span></span>

```JSON
{
  "name": "DocumentDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="43fcd-254">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="43fcd-254">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="43fcd-255">**Azure DocumentDB output dataset:**</span><span class="sxs-lookup"><span data-stu-id="43fcd-255">**Azure DocumentDB output dataset:**</span></span>

<span data-ttu-id="43fcd-256">The sample copies data to a collection named “Person”.</span><span class="sxs-lookup"><span data-stu-id="43fcd-256">The sample copies data to a collection named “Person”.</span></span>

```JSON
{
  "name": "PersonDocumentDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "DocumentDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="43fcd-257">The following pipeline copies data from Azure Blob to the Person collection in the DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="43fcd-257">The following pipeline copies data from Azure Blob to the Person collection in the DocumentDB.</span></span> <span data-ttu-id="43fcd-258">As part of the copy activity the input and output datasets have been specified.</span><span class="sxs-lookup"><span data-stu-id="43fcd-258">As part of the copy activity the input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonDocumentDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="43fcd-259">If the sample blob input is as</span><span class="sxs-lookup"><span data-stu-id="43fcd-259">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="43fcd-260">Then the output JSON in DocumentDB will be as:</span><span class="sxs-lookup"><span data-stu-id="43fcd-260">Then the output JSON in DocumentDB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="43fcd-261">DocumentDB is a NoSQL store for JSON documents, where nested structures are allowed.</span><span class="sxs-lookup"><span data-stu-id="43fcd-261">DocumentDB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="43fcd-262">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span><span class="sxs-lookup"><span data-stu-id="43fcd-262">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="43fcd-263">in this example.</span><span class="sxs-lookup"><span data-stu-id="43fcd-263">in this example.</span></span> <span data-ttu-id="43fcd-264">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span><span class="sxs-lookup"><span data-stu-id="43fcd-264">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="43fcd-265">Appendix</span><span class="sxs-lookup"><span data-stu-id="43fcd-265">Appendix</span></span>
1. <span data-ttu-id="43fcd-266">**Question:** Does the Copy Activity support update of existing records?</span><span class="sxs-lookup"><span data-stu-id="43fcd-266">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="43fcd-267">**Answer:** No.</span><span class="sxs-lookup"><span data-stu-id="43fcd-267">**Answer:** No.</span></span>
2. <span data-ttu-id="43fcd-268">**Question:** How does a retry of a copy to DocumentDB deal with already copied records?</span><span class="sxs-lookup"><span data-stu-id="43fcd-268">**Question:** How does a retry of a copy to DocumentDB deal with already copied records?</span></span>

    <span data-ttu-id="43fcd-269">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span><span class="sxs-lookup"><span data-stu-id="43fcd-269">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="43fcd-270">**Question:** Does Data Factory support [range or hash-based data partitioning](https://azure.microsoft.com/documentation/articles/documentdb-partition-data/)?</span><span class="sxs-lookup"><span data-stu-id="43fcd-270">**Question:** Does Data Factory support [range or hash-based data partitioning](https://azure.microsoft.com/documentation/articles/documentdb-partition-data/)?</span></span>

    <span data-ttu-id="43fcd-271">**Answer:** No.</span><span class="sxs-lookup"><span data-stu-id="43fcd-271">**Answer:** No.</span></span>
4. <span data-ttu-id="43fcd-272">**Question:** Can I specify more than one DocumentDB collection for a table?</span><span class="sxs-lookup"><span data-stu-id="43fcd-272">**Question:** Can I specify more than one DocumentDB collection for a table?</span></span>

    <span data-ttu-id="43fcd-273">**Answer:** No.</span><span class="sxs-lookup"><span data-stu-id="43fcd-273">**Answer:** No.</span></span> <span data-ttu-id="43fcd-274">Only one collection can be specified at this time.</span><span class="sxs-lookup"><span data-stu-id="43fcd-274">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="43fcd-275">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="43fcd-275">Performance and Tuning</span></span>
<span data-ttu-id="43fcd-276">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="43fcd-276">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
