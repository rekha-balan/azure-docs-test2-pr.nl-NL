---
title: Move data from Web Table using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from a table in a Web page using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/05/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 05833599059c2724529f9fd23edcd86934793835
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867959"
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="2806b-103">Move data from a Web table source using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2806b-103">Move data from a Web table source using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-web-table-connector.md)
> * [Version 2 (current version)](../connector-web-table.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Web table connector in V2](../connector-web-table.md).

<span data-ttu-id="2806b-108">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="2806b-108">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="2806b-109">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span><span class="sxs-lookup"><span data-stu-id="2806b-109">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="2806b-110">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span><span class="sxs-lookup"><span data-stu-id="2806b-110">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> This Web connector currently supports only extracting table content from an HTML page. To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.

## <a name="prerequisites"></a><span data-ttu-id="2806b-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2806b-113">Prerequisites</span></span>

<span data-ttu-id="2806b-114">To use this Web table connector, you need to set up a Self-hosted Integration Runtime (aka Data Management Gateway) and configure the `gatewayName` property in the sink linked service.</span><span class="sxs-lookup"><span data-stu-id="2806b-114">To use this Web table connector, you need to set up a Self-hosted Integration Runtime (aka Data Management Gateway) and configure the `gatewayName` property in the sink linked service.</span></span> <span data-ttu-id="2806b-115">For example, to copy from Web table to Azure Blob storage, configure the Azure Storage linked service as the following:</span><span class="sxs-lookup"><span data-stu-id="2806b-115">For example, to copy from Web table to Azure Blob storage, configure the Azure Storage linked service as the following:</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>",
      "gatewayName": "<gateway name>"
    }
  }
}
```

## <a name="getting-started"></a><span data-ttu-id="2806b-116">Getting started</span><span class="sxs-lookup"><span data-stu-id="2806b-116">Getting started</span></span>
<span data-ttu-id="2806b-117">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="2806b-117">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2806b-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="2806b-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="2806b-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="2806b-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="2806b-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="2806b-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2806b-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="2806b-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2806b-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="2806b-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="2806b-123">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="2806b-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="2806b-124">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="2806b-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="2806b-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="2806b-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2806b-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="2806b-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="2806b-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="2806b-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="2806b-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="2806b-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2806b-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span><span class="sxs-lookup"><span data-stu-id="2806b-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2806b-130">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="2806b-130">Linked service properties</span></span>
<span data-ttu-id="2806b-131">The following table provides description for JSON elements specific to Web linked service.</span><span class="sxs-lookup"><span data-stu-id="2806b-131">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="2806b-132">Property</span><span class="sxs-lookup"><span data-stu-id="2806b-132">Property</span></span> | <span data-ttu-id="2806b-133">Description</span><span class="sxs-lookup"><span data-stu-id="2806b-133">Description</span></span> | <span data-ttu-id="2806b-134">Required</span><span class="sxs-lookup"><span data-stu-id="2806b-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2806b-135">type</span><span class="sxs-lookup"><span data-stu-id="2806b-135">type</span></span> |<span data-ttu-id="2806b-136">The type property must be set to: **Web**</span><span class="sxs-lookup"><span data-stu-id="2806b-136">The type property must be set to: **Web**</span></span> |<span data-ttu-id="2806b-137">Yes</span><span class="sxs-lookup"><span data-stu-id="2806b-137">Yes</span></span> |
| <span data-ttu-id="2806b-138">Url</span><span class="sxs-lookup"><span data-stu-id="2806b-138">Url</span></span> |<span data-ttu-id="2806b-139">URL to the Web source</span><span class="sxs-lookup"><span data-stu-id="2806b-139">URL to the Web source</span></span> |<span data-ttu-id="2806b-140">Yes</span><span class="sxs-lookup"><span data-stu-id="2806b-140">Yes</span></span> |
| <span data-ttu-id="2806b-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2806b-141">authenticationType</span></span> |<span data-ttu-id="2806b-142">Anonymous.</span><span class="sxs-lookup"><span data-stu-id="2806b-142">Anonymous.</span></span> |<span data-ttu-id="2806b-143">Yes</span><span class="sxs-lookup"><span data-stu-id="2806b-143">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="2806b-144">Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="2806b-144">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="2806b-145">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="2806b-145">Dataset properties</span></span>
<span data-ttu-id="2806b-146">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="2806b-146">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2806b-147">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="2806b-147">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2806b-148">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="2806b-148">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="2806b-149">The typeProperties section for dataset of type **WebTable** has the following properties</span><span class="sxs-lookup"><span data-stu-id="2806b-149">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="2806b-150">Property</span><span class="sxs-lookup"><span data-stu-id="2806b-150">Property</span></span> | <span data-ttu-id="2806b-151">Description</span><span class="sxs-lookup"><span data-stu-id="2806b-151">Description</span></span> | <span data-ttu-id="2806b-152">Required</span><span class="sxs-lookup"><span data-stu-id="2806b-152">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2806b-153">type</span><span class="sxs-lookup"><span data-stu-id="2806b-153">type</span></span> |<span data-ttu-id="2806b-154">type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="2806b-154">type of the dataset.</span></span> <span data-ttu-id="2806b-155">must be set to **WebTable**</span><span class="sxs-lookup"><span data-stu-id="2806b-155">must be set to **WebTable**</span></span> |<span data-ttu-id="2806b-156">Yes</span><span class="sxs-lookup"><span data-stu-id="2806b-156">Yes</span></span> |
| <span data-ttu-id="2806b-157">path</span><span class="sxs-lookup"><span data-stu-id="2806b-157">path</span></span> |<span data-ttu-id="2806b-158">A relative URL to the resource that contains the table.</span><span class="sxs-lookup"><span data-stu-id="2806b-158">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="2806b-159">No.</span><span class="sxs-lookup"><span data-stu-id="2806b-159">No.</span></span> <span data-ttu-id="2806b-160">When path is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="2806b-160">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="2806b-161">index</span><span class="sxs-lookup"><span data-stu-id="2806b-161">index</span></span> |<span data-ttu-id="2806b-162">The index of the table in the resource.</span><span class="sxs-lookup"><span data-stu-id="2806b-162">The index of the table in the resource.</span></span> <span data-ttu-id="2806b-163">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span><span class="sxs-lookup"><span data-stu-id="2806b-163">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="2806b-164">Yes</span><span class="sxs-lookup"><span data-stu-id="2806b-164">Yes</span></span> |

<span data-ttu-id="2806b-165">**Example:**</span><span class="sxs-lookup"><span data-stu-id="2806b-165">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="2806b-166">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="2806b-166">Copy activity properties</span></span>
<span data-ttu-id="2806b-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="2806b-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2806b-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="2806b-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2806b-169">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="2806b-169">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="2806b-170">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="2806b-170">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="2806b-171">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span><span class="sxs-lookup"><span data-stu-id="2806b-171">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="2806b-172">JSON example: Copy data from Web table to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="2806b-172">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="2806b-173">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="2806b-173">The following sample shows:</span></span>

1. <span data-ttu-id="2806b-174">A linked service of type [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2806b-174">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="2806b-175">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2806b-175">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2806b-176">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2806b-176">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="2806b-177">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2806b-177">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2806b-178">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2806b-178">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2806b-179">The sample copies data from a Web table to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="2806b-179">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="2806b-180">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="2806b-180">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="2806b-181">The following sample shows how to copy data from a Web table to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="2806b-181">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="2806b-182">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2806b-182">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="2806b-183">**Web linked service** This example uses the Web linked service with anonymous authentication.</span><span class="sxs-lookup"><span data-stu-id="2806b-183">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="2806b-184">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="2806b-184">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="2806b-185">**Azure Storage linked service**</span><span class="sxs-lookup"><span data-stu-id="2806b-185">**Azure Storage linked service**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>",
      "gatewayName": "<gateway name>"
    }
  }
}
```

<span data-ttu-id="2806b-186">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="2806b-186">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="2806b-188">**Azure Blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="2806b-188">**Azure Blob output dataset**</span></span>

<span data-ttu-id="2806b-189">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="2806b-189">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="2806b-190">**Pipeline with Copy activity**</span><span class="sxs-lookup"><span data-stu-id="2806b-190">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="2806b-191">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="2806b-191">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2806b-192">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2806b-192">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="2806b-193">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span><span class="sxs-lookup"><span data-stu-id="2806b-193">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="2806b-194">Get index of a table in an HTML page</span><span class="sxs-lookup"><span data-stu-id="2806b-194">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="2806b-195">Launch **Excel 2016** and switch to the **Data** tab.</span><span class="sxs-lookup"><span data-stu-id="2806b-195">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="2806b-196">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span><span class="sxs-lookup"><span data-stu-id="2806b-196">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Power Query menu](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="2806b-198">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2806b-198">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![From Web dialog](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="2806b-200">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="2806b-200">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="2806b-201">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="2806b-201">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Access Web content dialog box](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="2806b-203">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2806b-203">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Navigator dialog](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="2806b-205">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="2806b-205">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Advanced Editor button](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="2806b-207">In the Advanced Editor dialog box, the number next to "Source" is the index.</span><span class="sxs-lookup"><span data-stu-id="2806b-207">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Advanced Editor - Index](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="2806b-209">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span><span class="sxs-lookup"><span data-stu-id="2806b-209">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="2806b-210">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span><span class="sxs-lookup"><span data-stu-id="2806b-210">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="2806b-211">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="2806b-211">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a><span data-ttu-id="2806b-213">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="2806b-213">Performance and Tuning</span></span>
<span data-ttu-id="2806b-214">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="2806b-214">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
