---
title: Move data from Web Table using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from a table in a Web page using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: jingwang
ms.openlocfilehash: e7e784e87478983424183f4af3726689bb3fb4f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660670"
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="49723-103">Move data from a Web table source using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="49723-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="49723-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="49723-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="49723-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span><span class="sxs-lookup"><span data-stu-id="49723-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="49723-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span><span class="sxs-lookup"><span data-stu-id="49723-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49723-107">This Web connector currently supports only extracting table content from an HTML page.</span><span class="sxs-lookup"><span data-stu-id="49723-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="49723-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span><span class="sxs-lookup"><span data-stu-id="49723-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="49723-109">Getting started</span><span class="sxs-lookup"><span data-stu-id="49723-109">Getting started</span></span>
<span data-ttu-id="49723-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="49723-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="49723-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="49723-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="49723-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="49723-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="49723-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="49723-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="49723-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="49723-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="49723-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="49723-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="49723-116">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="49723-116">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="49723-117">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="49723-117">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="49723-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="49723-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="49723-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="49723-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="49723-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="49723-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="49723-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="49723-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="49723-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span><span class="sxs-lookup"><span data-stu-id="49723-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="49723-123">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="49723-123">Linked service properties</span></span>
<span data-ttu-id="49723-124">The following table provides description for JSON elements specific to Web linked service.</span><span class="sxs-lookup"><span data-stu-id="49723-124">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="49723-125">Property</span><span class="sxs-lookup"><span data-stu-id="49723-125">Property</span></span> | <span data-ttu-id="49723-126">Description</span><span class="sxs-lookup"><span data-stu-id="49723-126">Description</span></span> | <span data-ttu-id="49723-127">Required</span><span class="sxs-lookup"><span data-stu-id="49723-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49723-128">type</span><span class="sxs-lookup"><span data-stu-id="49723-128">type</span></span> |<span data-ttu-id="49723-129">The type property must be set to: **Web**</span><span class="sxs-lookup"><span data-stu-id="49723-129">The type property must be set to: **Web**</span></span> |<span data-ttu-id="49723-130">Yes</span><span class="sxs-lookup"><span data-stu-id="49723-130">Yes</span></span> |
| <span data-ttu-id="49723-131">Url</span><span class="sxs-lookup"><span data-stu-id="49723-131">Url</span></span> |<span data-ttu-id="49723-132">URL to the Web source</span><span class="sxs-lookup"><span data-stu-id="49723-132">URL to the Web source</span></span> |<span data-ttu-id="49723-133">Yes</span><span class="sxs-lookup"><span data-stu-id="49723-133">Yes</span></span> |
| <span data-ttu-id="49723-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="49723-134">authenticationType</span></span> |<span data-ttu-id="49723-135">Anonymous.</span><span class="sxs-lookup"><span data-stu-id="49723-135">Anonymous.</span></span> |<span data-ttu-id="49723-136">Yes</span><span class="sxs-lookup"><span data-stu-id="49723-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="49723-137">Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="49723-137">Using Anonymous authentication</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="49723-138">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="49723-138">Dataset properties</span></span>
<span data-ttu-id="49723-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="49723-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="49723-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="49723-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="49723-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="49723-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="49723-142">The typeProperties section for dataset of type **WebTable** has the following properties</span><span class="sxs-lookup"><span data-stu-id="49723-142">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="49723-143">Property</span><span class="sxs-lookup"><span data-stu-id="49723-143">Property</span></span> | <span data-ttu-id="49723-144">Description</span><span class="sxs-lookup"><span data-stu-id="49723-144">Description</span></span> | <span data-ttu-id="49723-145">Required</span><span class="sxs-lookup"><span data-stu-id="49723-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="49723-146">type</span><span class="sxs-lookup"><span data-stu-id="49723-146">type</span></span> |<span data-ttu-id="49723-147">type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="49723-147">type of the dataset.</span></span> <span data-ttu-id="49723-148">must be set to **WebTable**</span><span class="sxs-lookup"><span data-stu-id="49723-148">must be set to **WebTable**</span></span> |<span data-ttu-id="49723-149">Yes</span><span class="sxs-lookup"><span data-stu-id="49723-149">Yes</span></span> |
| <span data-ttu-id="49723-150">path</span><span class="sxs-lookup"><span data-stu-id="49723-150">path</span></span> |<span data-ttu-id="49723-151">A relative URL to the resource that contains the table.</span><span class="sxs-lookup"><span data-stu-id="49723-151">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="49723-152">No.</span><span class="sxs-lookup"><span data-stu-id="49723-152">No.</span></span> <span data-ttu-id="49723-153">When path is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="49723-153">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="49723-154">index</span><span class="sxs-lookup"><span data-stu-id="49723-154">index</span></span> |<span data-ttu-id="49723-155">The index of the table in the resource.</span><span class="sxs-lookup"><span data-stu-id="49723-155">The index of the table in the resource.</span></span> <span data-ttu-id="49723-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span><span class="sxs-lookup"><span data-stu-id="49723-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="49723-157">Yes</span><span class="sxs-lookup"><span data-stu-id="49723-157">Yes</span></span> |

<span data-ttu-id="49723-158">**Example:**</span><span class="sxs-lookup"><span data-stu-id="49723-158">**Example:**</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="49723-159">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="49723-159">Copy activity properties</span></span>
<span data-ttu-id="49723-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="49723-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="49723-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="49723-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="49723-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="49723-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="49723-163">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="49723-163">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="49723-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span><span class="sxs-lookup"><span data-stu-id="49723-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="49723-165">JSON example: Copy data from Web table to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="49723-165">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="49723-166">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="49723-166">The following sample shows:</span></span>

1. <span data-ttu-id="49723-167">A linked service of type [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="49723-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="49723-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="49723-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="49723-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="49723-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="49723-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="49723-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="49723-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="49723-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="49723-172">The sample copies data from a Web table to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="49723-172">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="49723-173">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="49723-173">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="49723-174">The following sample shows how to copy data from a Web table to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="49723-174">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="49723-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="49723-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="49723-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span><span class="sxs-lookup"><span data-stu-id="49723-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="49723-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="49723-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="49723-178">**Azure Storage linked service**</span><span class="sxs-lookup"><span data-stu-id="49723-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="49723-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="49723-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="49723-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span><span class="sxs-lookup"><span data-stu-id="49723-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span>  
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


<span data-ttu-id="49723-181">**Azure Blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="49723-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="49723-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="49723-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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



<span data-ttu-id="49723-183">**Pipeline with Copy activity**</span><span class="sxs-lookup"><span data-stu-id="49723-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="49723-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="49723-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="49723-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="49723-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="49723-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span><span class="sxs-lookup"><span data-stu-id="49723-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="49723-187">Get index of a table in an HTML page</span><span class="sxs-lookup"><span data-stu-id="49723-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="49723-188">Launch **Excel 2016** and switch to the **Data** tab.</span><span class="sxs-lookup"><span data-stu-id="49723-188">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="49723-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span><span class="sxs-lookup"><span data-stu-id="49723-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Power Query menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="49723-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="49723-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![From Web dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="49723-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="49723-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="49723-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="49723-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Access Web content dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="49723-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="49723-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Navigator dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="49723-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="49723-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Advanced Editor button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="49723-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span><span class="sxs-lookup"><span data-stu-id="49723-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Advanced Editor - Index](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="49723-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span><span class="sxs-lookup"><span data-stu-id="49723-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="49723-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span><span class="sxs-lookup"><span data-stu-id="49723-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="49723-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="49723-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="49723-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="49723-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="49723-206">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="49723-206">Performance and Tuning</span></span>
<span data-ttu-id="49723-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="49723-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>






