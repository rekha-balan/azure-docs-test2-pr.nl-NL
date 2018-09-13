---
title: Move data from Amazon Redshift using Data Factory | Microsoft Docs
description: Learn about how to move data from Amazon Redshift using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: jingwang
ms.openlocfilehash: 524b87d95d3060c780b296350797501847c80638
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555717"
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="f8111-103">Move data From Amazon Redshift using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f8111-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="f8111-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="f8111-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="f8111-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="f8111-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="f8111-106">You can copy data from Amazon Redshift to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f8111-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="f8111-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="f8111-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="f8111-108">Data factory currently supports only moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="f8111-108">Data factory currently supports only moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8111-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f8111-109">Prerequisites</span></span>
* <span data-ttu-id="f8111-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="f8111-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="f8111-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span><span class="sxs-lookup"><span data-stu-id="f8111-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="f8111-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span><span class="sxs-lookup"><span data-stu-id="f8111-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="f8111-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address ranges (including SQL ranges) used by the Microsoft Azure data centers.</span><span class="sxs-lookup"><span data-stu-id="f8111-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address ranges (including SQL ranges) used by the Microsoft Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f8111-114">Getting started</span><span class="sxs-lookup"><span data-stu-id="f8111-114">Getting started</span></span>
<span data-ttu-id="f8111-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="f8111-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="f8111-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="f8111-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f8111-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="f8111-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="f8111-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="f8111-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f8111-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="f8111-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f8111-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="f8111-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="f8111-121">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f8111-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="f8111-122">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="f8111-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="f8111-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="f8111-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f8111-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="f8111-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="f8111-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="f8111-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="f8111-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="f8111-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="f8111-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="f8111-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="f8111-128">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f8111-128">Linked service properties</span></span>
<span data-ttu-id="f8111-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span><span class="sxs-lookup"><span data-stu-id="f8111-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="f8111-130">Property</span><span class="sxs-lookup"><span data-stu-id="f8111-130">Property</span></span> | <span data-ttu-id="f8111-131">Description</span><span class="sxs-lookup"><span data-stu-id="f8111-131">Description</span></span> | <span data-ttu-id="f8111-132">Required</span><span class="sxs-lookup"><span data-stu-id="f8111-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f8111-133">type</span><span class="sxs-lookup"><span data-stu-id="f8111-133">type</span></span> |<span data-ttu-id="f8111-134">The type property must be set to: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="f8111-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="f8111-135">Yes</span><span class="sxs-lookup"><span data-stu-id="f8111-135">Yes</span></span> |
| <span data-ttu-id="f8111-136">server</span><span class="sxs-lookup"><span data-stu-id="f8111-136">server</span></span> |<span data-ttu-id="f8111-137">IP address or host name of the Amazon Redshift server.</span><span class="sxs-lookup"><span data-stu-id="f8111-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="f8111-138">Yes</span><span class="sxs-lookup"><span data-stu-id="f8111-138">Yes</span></span> |
| <span data-ttu-id="f8111-139">port</span><span class="sxs-lookup"><span data-stu-id="f8111-139">port</span></span> |<span data-ttu-id="f8111-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="f8111-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="f8111-141">No, default value: 5439</span><span class="sxs-lookup"><span data-stu-id="f8111-141">No, default value: 5439</span></span> |
| <span data-ttu-id="f8111-142">database</span><span class="sxs-lookup"><span data-stu-id="f8111-142">database</span></span> |<span data-ttu-id="f8111-143">Name of the Amazon Redshift database.</span><span class="sxs-lookup"><span data-stu-id="f8111-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="f8111-144">Yes</span><span class="sxs-lookup"><span data-stu-id="f8111-144">Yes</span></span> |
| <span data-ttu-id="f8111-145">username</span><span class="sxs-lookup"><span data-stu-id="f8111-145">username</span></span> |<span data-ttu-id="f8111-146">Name of user who has access to the database.</span><span class="sxs-lookup"><span data-stu-id="f8111-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="f8111-147">Yes</span><span class="sxs-lookup"><span data-stu-id="f8111-147">Yes</span></span> |
| <span data-ttu-id="f8111-148">password</span><span class="sxs-lookup"><span data-stu-id="f8111-148">password</span></span> |<span data-ttu-id="f8111-149">Password for the user account.</span><span class="sxs-lookup"><span data-stu-id="f8111-149">Password for the user account.</span></span> |<span data-ttu-id="f8111-150">Yes</span><span class="sxs-lookup"><span data-stu-id="f8111-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="f8111-151">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f8111-151">Dataset properties</span></span>
<span data-ttu-id="f8111-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="f8111-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f8111-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="f8111-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f8111-154">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="f8111-154">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f8111-155">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span><span class="sxs-lookup"><span data-stu-id="f8111-155">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="f8111-156">Property</span><span class="sxs-lookup"><span data-stu-id="f8111-156">Property</span></span> | <span data-ttu-id="f8111-157">Description</span><span class="sxs-lookup"><span data-stu-id="f8111-157">Description</span></span> | <span data-ttu-id="f8111-158">Required</span><span class="sxs-lookup"><span data-stu-id="f8111-158">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f8111-159">tableName</span><span class="sxs-lookup"><span data-stu-id="f8111-159">tableName</span></span> |<span data-ttu-id="f8111-160">Name of the table in the Amazon Redshift database that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="f8111-160">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="f8111-161">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="f8111-161">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f8111-162">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f8111-162">Copy activity properties</span></span>
<span data-ttu-id="f8111-163">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="f8111-163">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f8111-164">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="f8111-164">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="f8111-165">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="f8111-165">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="f8111-166">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="f8111-166">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="f8111-167">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift) the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="f8111-167">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="f8111-168">Property</span><span class="sxs-lookup"><span data-stu-id="f8111-168">Property</span></span> | <span data-ttu-id="f8111-169">Description</span><span class="sxs-lookup"><span data-stu-id="f8111-169">Description</span></span> | <span data-ttu-id="f8111-170">Allowed values</span><span class="sxs-lookup"><span data-stu-id="f8111-170">Allowed values</span></span> | <span data-ttu-id="f8111-171">Required</span><span class="sxs-lookup"><span data-stu-id="f8111-171">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f8111-172">query</span><span class="sxs-lookup"><span data-stu-id="f8111-172">query</span></span> |<span data-ttu-id="f8111-173">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="f8111-173">Use the custom query to read data.</span></span> |<span data-ttu-id="f8111-174">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="f8111-174">SQL query string.</span></span> <span data-ttu-id="f8111-175">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="f8111-175">For example: select \* from MyTable.</span></span> |<span data-ttu-id="f8111-176">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="f8111-176">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="f8111-177">JSON example: Copy data from Amazon Redshift to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="f8111-177">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="f8111-178">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f8111-178">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="f8111-179">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f8111-179">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="f8111-180">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="f8111-180">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="f8111-181">A linked service of type [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f8111-181">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="f8111-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f8111-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="f8111-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f8111-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="f8111-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f8111-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="f8111-185">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f8111-185">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="f8111-186">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="f8111-186">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="f8111-187">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="f8111-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f8111-188">**Amazon Redshift linked service:**</span><span class="sxs-lookup"><span data-stu-id="f8111-188">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="f8111-189">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="f8111-189">**Azure Storage linked service:**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="f8111-190">**Amazon Redshift input dataset:**</span><span class="sxs-lookup"><span data-stu-id="f8111-190">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="f8111-191">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f8111-191">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="f8111-192">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f8111-192">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="f8111-193">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="f8111-193">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f8111-194">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f8111-194">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f8111-195">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="f8111-195">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f8111-196">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="f8111-196">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="f8111-197">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="f8111-197">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="f8111-198">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="f8111-198">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f8111-199">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f8111-199">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f8111-200">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="f8111-200">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="f8111-201">Type mapping for Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="f8111-201">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="f8111-202">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span><span class="sxs-lookup"><span data-stu-id="f8111-202">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="f8111-203">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="f8111-203">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f8111-204">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="f8111-204">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f8111-205">When moving data to Amazon Redshift, the following mappings will be used from Amazon Redshift types to .NET types.</span><span class="sxs-lookup"><span data-stu-id="f8111-205">When moving data to Amazon Redshift, the following mappings will be used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="f8111-206">Amazon Redshift Type</span><span class="sxs-lookup"><span data-stu-id="f8111-206">Amazon Redshift Type</span></span> | <span data-ttu-id="f8111-207">.NET Based Type</span><span class="sxs-lookup"><span data-stu-id="f8111-207">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="f8111-208">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="f8111-208">SMALLINT</span></span> |<span data-ttu-id="f8111-209">Int16</span><span class="sxs-lookup"><span data-stu-id="f8111-209">Int16</span></span> |
| <span data-ttu-id="f8111-210">INTEGER</span><span class="sxs-lookup"><span data-stu-id="f8111-210">INTEGER</span></span> |<span data-ttu-id="f8111-211">Int32</span><span class="sxs-lookup"><span data-stu-id="f8111-211">Int32</span></span> |
| <span data-ttu-id="f8111-212">BIGINT</span><span class="sxs-lookup"><span data-stu-id="f8111-212">BIGINT</span></span> |<span data-ttu-id="f8111-213">Int64</span><span class="sxs-lookup"><span data-stu-id="f8111-213">Int64</span></span> |
| <span data-ttu-id="f8111-214">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="f8111-214">DECIMAL</span></span> |<span data-ttu-id="f8111-215">Decimal</span><span class="sxs-lookup"><span data-stu-id="f8111-215">Decimal</span></span> |
| <span data-ttu-id="f8111-216">REAL</span><span class="sxs-lookup"><span data-stu-id="f8111-216">REAL</span></span> |<span data-ttu-id="f8111-217">Single</span><span class="sxs-lookup"><span data-stu-id="f8111-217">Single</span></span> |
| <span data-ttu-id="f8111-218">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="f8111-218">DOUBLE PRECISION</span></span> |<span data-ttu-id="f8111-219">Double</span><span class="sxs-lookup"><span data-stu-id="f8111-219">Double</span></span> |
| <span data-ttu-id="f8111-220">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="f8111-220">BOOLEAN</span></span> |<span data-ttu-id="f8111-221">String</span><span class="sxs-lookup"><span data-stu-id="f8111-221">String</span></span> |
| <span data-ttu-id="f8111-222">CHAR</span><span class="sxs-lookup"><span data-stu-id="f8111-222">CHAR</span></span> |<span data-ttu-id="f8111-223">String</span><span class="sxs-lookup"><span data-stu-id="f8111-223">String</span></span> |
| <span data-ttu-id="f8111-224">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="f8111-224">VARCHAR</span></span> |<span data-ttu-id="f8111-225">String</span><span class="sxs-lookup"><span data-stu-id="f8111-225">String</span></span> |
| <span data-ttu-id="f8111-226">DATE</span><span class="sxs-lookup"><span data-stu-id="f8111-226">DATE</span></span> |<span data-ttu-id="f8111-227">DateTime</span><span class="sxs-lookup"><span data-stu-id="f8111-227">DateTime</span></span> |
| <span data-ttu-id="f8111-228">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="f8111-228">TIMESTAMP</span></span> |<span data-ttu-id="f8111-229">DateTime</span><span class="sxs-lookup"><span data-stu-id="f8111-229">DateTime</span></span> |
| <span data-ttu-id="f8111-230">TEXT</span><span class="sxs-lookup"><span data-stu-id="f8111-230">TEXT</span></span> |<span data-ttu-id="f8111-231">String</span><span class="sxs-lookup"><span data-stu-id="f8111-231">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="f8111-232">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="f8111-232">Map source to sink columns</span></span>
<span data-ttu-id="f8111-233">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f8111-233">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="f8111-234">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="f8111-234">Repeatable read from relational sources</span></span>
<span data-ttu-id="f8111-235">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="f8111-235">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="f8111-236">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="f8111-236">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f8111-237">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="f8111-237">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f8111-238">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="f8111-238">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f8111-239">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="f8111-239">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f8111-240">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="f8111-240">Performance and Tuning</span></span>
<span data-ttu-id="f8111-241">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="f8111-241">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8111-242">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f8111-242">Next Steps</span></span>
<span data-ttu-id="f8111-243">See the following articles:</span><span class="sxs-lookup"><span data-stu-id="f8111-243">See the following articles:</span></span>

* <span data-ttu-id="f8111-244">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="f8111-244">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
