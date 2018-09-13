---
title: Move data from Teradata using Azure Data Factory | Microsoft Docs
description: Learn about Teradata Connector for the Data Factory service that lets you move data from Teradata Database
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: jingwang
ms.openlocfilehash: fdbf0a885e98070732ca520cf13d36c255a81790
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660969"
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="b5da1-103">Move data from Teradata using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b5da1-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="b5da1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span><span class="sxs-lookup"><span data-stu-id="b5da1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="b5da1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="b5da1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="b5da1-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="b5da1-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="b5da1-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="b5da1-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="b5da1-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span><span class="sxs-lookup"><span data-stu-id="b5da1-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b5da1-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b5da1-109">Prerequisites</span></span>
<span data-ttu-id="b5da1-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="b5da1-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="b5da1-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="b5da1-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="b5da1-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b5da1-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="b5da1-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="b5da1-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="b5da1-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="b5da1-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="b5da1-115">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="b5da1-115">Supported versions and installation</span></span>
<span data-ttu-id="b5da1-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="b5da1-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="b5da1-117">Teradata version 12 and above is supported.</span><span class="sxs-lookup"><span data-stu-id="b5da1-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b5da1-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="b5da1-118">Getting started</span></span>
<span data-ttu-id="b5da1-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="b5da1-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="b5da1-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="b5da1-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b5da1-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="b5da1-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="b5da1-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="b5da1-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b5da1-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="b5da1-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b5da1-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="b5da1-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="b5da1-125">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="b5da1-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="b5da1-126">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="b5da1-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="b5da1-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="b5da1-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b5da1-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="b5da1-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b5da1-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="b5da1-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b5da1-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="b5da1-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="b5da1-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span><span class="sxs-lookup"><span data-stu-id="b5da1-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b5da1-132">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="b5da1-132">Linked service properties</span></span>
<span data-ttu-id="b5da1-133">The following table provides description for JSON elements specific to Teradata linked service.</span><span class="sxs-lookup"><span data-stu-id="b5da1-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="b5da1-134">Property</span><span class="sxs-lookup"><span data-stu-id="b5da1-134">Property</span></span> | <span data-ttu-id="b5da1-135">Description</span><span class="sxs-lookup"><span data-stu-id="b5da1-135">Description</span></span> | <span data-ttu-id="b5da1-136">Required</span><span class="sxs-lookup"><span data-stu-id="b5da1-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5da1-137">type</span><span class="sxs-lookup"><span data-stu-id="b5da1-137">type</span></span> |<span data-ttu-id="b5da1-138">The type property must be set to: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="b5da1-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="b5da1-139">Yes</span><span class="sxs-lookup"><span data-stu-id="b5da1-139">Yes</span></span> |
| <span data-ttu-id="b5da1-140">server</span><span class="sxs-lookup"><span data-stu-id="b5da1-140">server</span></span> |<span data-ttu-id="b5da1-141">Name of the Teradata server.</span><span class="sxs-lookup"><span data-stu-id="b5da1-141">Name of the Teradata server.</span></span> |<span data-ttu-id="b5da1-142">Yes</span><span class="sxs-lookup"><span data-stu-id="b5da1-142">Yes</span></span> |
| <span data-ttu-id="b5da1-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="b5da1-143">authenticationType</span></span> |<span data-ttu-id="b5da1-144">Type of authentication used to connect to the Teradata database.</span><span class="sxs-lookup"><span data-stu-id="b5da1-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="b5da1-145">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="b5da1-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="b5da1-146">Yes</span><span class="sxs-lookup"><span data-stu-id="b5da1-146">Yes</span></span> |
| <span data-ttu-id="b5da1-147">username</span><span class="sxs-lookup"><span data-stu-id="b5da1-147">username</span></span> |<span data-ttu-id="b5da1-148">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="b5da1-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="b5da1-149">No</span><span class="sxs-lookup"><span data-stu-id="b5da1-149">No</span></span> |
| <span data-ttu-id="b5da1-150">password</span><span class="sxs-lookup"><span data-stu-id="b5da1-150">password</span></span> |<span data-ttu-id="b5da1-151">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="b5da1-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="b5da1-152">No</span><span class="sxs-lookup"><span data-stu-id="b5da1-152">No</span></span> |
| <span data-ttu-id="b5da1-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b5da1-153">gatewayName</span></span> |<span data-ttu-id="b5da1-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span><span class="sxs-lookup"><span data-stu-id="b5da1-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="b5da1-155">Yes</span><span class="sxs-lookup"><span data-stu-id="b5da1-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="b5da1-156">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="b5da1-156">Dataset properties</span></span>
<span data-ttu-id="b5da1-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="b5da1-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b5da1-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="b5da1-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b5da1-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="b5da1-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="b5da1-160">Currently, there are no type properties supported for the Teradata dataset.</span><span class="sxs-lookup"><span data-stu-id="b5da1-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="b5da1-161">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="b5da1-161">Copy activity properties</span></span>
<span data-ttu-id="b5da1-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="b5da1-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b5da1-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="b5da1-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="b5da1-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="b5da1-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="b5da1-165">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="b5da1-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="b5da1-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="b5da1-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="b5da1-167">Property</span><span class="sxs-lookup"><span data-stu-id="b5da1-167">Property</span></span> | <span data-ttu-id="b5da1-168">Description</span><span class="sxs-lookup"><span data-stu-id="b5da1-168">Description</span></span> | <span data-ttu-id="b5da1-169">Allowed values</span><span class="sxs-lookup"><span data-stu-id="b5da1-169">Allowed values</span></span> | <span data-ttu-id="b5da1-170">Required</span><span class="sxs-lookup"><span data-stu-id="b5da1-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b5da1-171">query</span><span class="sxs-lookup"><span data-stu-id="b5da1-171">query</span></span> |<span data-ttu-id="b5da1-172">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="b5da1-172">Use the custom query to read data.</span></span> |<span data-ttu-id="b5da1-173">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="b5da1-173">SQL query string.</span></span> <span data-ttu-id="b5da1-174">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="b5da1-174">For example: select \* from MyTable.</span></span> |<span data-ttu-id="b5da1-175">Yes</span><span class="sxs-lookup"><span data-stu-id="b5da1-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="b5da1-176">JSON example: Copy data from Teradata to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="b5da1-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="b5da1-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b5da1-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b5da1-178">They show how to copy data from Teradata to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b5da1-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="b5da1-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b5da1-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="b5da1-180">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="b5da1-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="b5da1-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b5da1-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="b5da1-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b5da1-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b5da1-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b5da1-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b5da1-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b5da1-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b5da1-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b5da1-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b5da1-186">The sample copies data from a query result in Teradata database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="b5da1-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="b5da1-187">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="b5da1-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b5da1-188">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="b5da1-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="b5da1-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="b5da1-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b5da1-190">**Teradata linked service:**</span><span class="sxs-lookup"><span data-stu-id="b5da1-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="b5da1-191">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="b5da1-191">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="b5da1-192">**Teradata input dataset:**</span><span class="sxs-lookup"><span data-stu-id="b5da1-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="b5da1-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span><span class="sxs-lookup"><span data-stu-id="b5da1-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="b5da1-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="b5da1-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="b5da1-195">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="b5da1-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="b5da1-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="b5da1-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b5da1-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="b5da1-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b5da1-198">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="b5da1-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="b5da1-199">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="b5da1-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="b5da1-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span><span class="sxs-lookup"><span data-stu-id="b5da1-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="b5da1-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b5da1-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b5da1-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="b5da1-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="b5da1-203">Type mapping for Teradata</span><span class="sxs-lookup"><span data-stu-id="b5da1-203">Type mapping for Teradata</span></span>
<span data-ttu-id="b5da1-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="b5da1-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="b5da1-205">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="b5da1-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="b5da1-206">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="b5da1-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="b5da1-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span><span class="sxs-lookup"><span data-stu-id="b5da1-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="b5da1-208">Teradata Database type</span><span class="sxs-lookup"><span data-stu-id="b5da1-208">Teradata Database type</span></span> | <span data-ttu-id="b5da1-209">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="b5da1-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b5da1-210">Char</span><span class="sxs-lookup"><span data-stu-id="b5da1-210">Char</span></span> |<span data-ttu-id="b5da1-211">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-211">String</span></span> |
| <span data-ttu-id="b5da1-212">Clob</span><span class="sxs-lookup"><span data-stu-id="b5da1-212">Clob</span></span> |<span data-ttu-id="b5da1-213">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-213">String</span></span> |
| <span data-ttu-id="b5da1-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="b5da1-214">Graphic</span></span> |<span data-ttu-id="b5da1-215">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-215">String</span></span> |
| <span data-ttu-id="b5da1-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="b5da1-216">VarChar</span></span> |<span data-ttu-id="b5da1-217">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-217">String</span></span> |
| <span data-ttu-id="b5da1-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="b5da1-218">VarGraphic</span></span> |<span data-ttu-id="b5da1-219">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-219">String</span></span> |
| <span data-ttu-id="b5da1-220">Blob</span><span class="sxs-lookup"><span data-stu-id="b5da1-220">Blob</span></span> |<span data-ttu-id="b5da1-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5da1-221">Byte[]</span></span> |
| <span data-ttu-id="b5da1-222">Byte</span><span class="sxs-lookup"><span data-stu-id="b5da1-222">Byte</span></span> |<span data-ttu-id="b5da1-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5da1-223">Byte[]</span></span> |
| <span data-ttu-id="b5da1-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="b5da1-224">VarByte</span></span> |<span data-ttu-id="b5da1-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5da1-225">Byte[]</span></span> |
| <span data-ttu-id="b5da1-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="b5da1-226">BigInt</span></span> |<span data-ttu-id="b5da1-227">Int64</span><span class="sxs-lookup"><span data-stu-id="b5da1-227">Int64</span></span> |
| <span data-ttu-id="b5da1-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="b5da1-228">ByteInt</span></span> |<span data-ttu-id="b5da1-229">Int16</span><span class="sxs-lookup"><span data-stu-id="b5da1-229">Int16</span></span> |
| <span data-ttu-id="b5da1-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5da1-230">Decimal</span></span> |<span data-ttu-id="b5da1-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5da1-231">Decimal</span></span> |
| <span data-ttu-id="b5da1-232">Double</span><span class="sxs-lookup"><span data-stu-id="b5da1-232">Double</span></span> |<span data-ttu-id="b5da1-233">Double</span><span class="sxs-lookup"><span data-stu-id="b5da1-233">Double</span></span> |
| <span data-ttu-id="b5da1-234">Integer</span><span class="sxs-lookup"><span data-stu-id="b5da1-234">Integer</span></span> |<span data-ttu-id="b5da1-235">Int32</span><span class="sxs-lookup"><span data-stu-id="b5da1-235">Int32</span></span> |
| <span data-ttu-id="b5da1-236">Number</span><span class="sxs-lookup"><span data-stu-id="b5da1-236">Number</span></span> |<span data-ttu-id="b5da1-237">Double</span><span class="sxs-lookup"><span data-stu-id="b5da1-237">Double</span></span> |
| <span data-ttu-id="b5da1-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b5da1-238">SmallInt</span></span> |<span data-ttu-id="b5da1-239">Int16</span><span class="sxs-lookup"><span data-stu-id="b5da1-239">Int16</span></span> |
| <span data-ttu-id="b5da1-240">Date</span><span class="sxs-lookup"><span data-stu-id="b5da1-240">Date</span></span> |<span data-ttu-id="b5da1-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="b5da1-241">DateTime</span></span> |
| <span data-ttu-id="b5da1-242">Time</span><span class="sxs-lookup"><span data-stu-id="b5da1-242">Time</span></span> |<span data-ttu-id="b5da1-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-243">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="b5da1-244">Time With Time Zone</span></span> |<span data-ttu-id="b5da1-245">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-245">String</span></span> |
| <span data-ttu-id="b5da1-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="b5da1-246">Timestamp</span></span> |<span data-ttu-id="b5da1-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="b5da1-247">DateTime</span></span> |
| <span data-ttu-id="b5da1-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="b5da1-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="b5da1-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="b5da1-249">DateTimeOffset</span></span> |
| <span data-ttu-id="b5da1-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="b5da1-250">Interval Day</span></span> |<span data-ttu-id="b5da1-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-251">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-252">Interval Day To Hour</span><span class="sxs-lookup"><span data-stu-id="b5da1-252">Interval Day To Hour</span></span> |<span data-ttu-id="b5da1-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-253">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-254">Interval Day To Minute</span><span class="sxs-lookup"><span data-stu-id="b5da1-254">Interval Day To Minute</span></span> |<span data-ttu-id="b5da1-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-255">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-256">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="b5da1-256">Interval Day To Second</span></span> |<span data-ttu-id="b5da1-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-257">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="b5da1-258">Interval Hour</span></span> |<span data-ttu-id="b5da1-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-259">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-260">Interval Hour To Minute</span><span class="sxs-lookup"><span data-stu-id="b5da1-260">Interval Hour To Minute</span></span> |<span data-ttu-id="b5da1-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-261">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-262">Interval Hour To Second</span><span class="sxs-lookup"><span data-stu-id="b5da1-262">Interval Hour To Second</span></span> |<span data-ttu-id="b5da1-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-263">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="b5da1-264">Interval Minute</span></span> |<span data-ttu-id="b5da1-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-265">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-266">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="b5da1-266">Interval Minute To Second</span></span> |<span data-ttu-id="b5da1-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-267">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="b5da1-268">Interval Second</span></span> |<span data-ttu-id="b5da1-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b5da1-269">TimeSpan</span></span> |
| <span data-ttu-id="b5da1-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="b5da1-270">Interval Year</span></span> |<span data-ttu-id="b5da1-271">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-271">String</span></span> |
| <span data-ttu-id="b5da1-272">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="b5da1-272">Interval Year To Month</span></span> |<span data-ttu-id="b5da1-273">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-273">String</span></span> |
| <span data-ttu-id="b5da1-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="b5da1-274">Interval Month</span></span> |<span data-ttu-id="b5da1-275">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-275">String</span></span> |
| <span data-ttu-id="b5da1-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="b5da1-276">Period(Date)</span></span> |<span data-ttu-id="b5da1-277">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-277">String</span></span> |
| <span data-ttu-id="b5da1-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="b5da1-278">Period(Time)</span></span> |<span data-ttu-id="b5da1-279">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-279">String</span></span> |
| <span data-ttu-id="b5da1-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="b5da1-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="b5da1-281">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-281">String</span></span> |
| <span data-ttu-id="b5da1-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="b5da1-282">Period(Timestamp)</span></span> |<span data-ttu-id="b5da1-283">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-283">String</span></span> |
| <span data-ttu-id="b5da1-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="b5da1-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="b5da1-285">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-285">String</span></span> |
| <span data-ttu-id="b5da1-286">Xml</span><span class="sxs-lookup"><span data-stu-id="b5da1-286">Xml</span></span> |<span data-ttu-id="b5da1-287">String</span><span class="sxs-lookup"><span data-stu-id="b5da1-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="b5da1-288">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="b5da1-288">Map source to sink columns</span></span>
<span data-ttu-id="b5da1-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b5da1-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="b5da1-290">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="b5da1-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="b5da1-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="b5da1-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="b5da1-292">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="b5da1-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b5da1-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="b5da1-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="b5da1-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="b5da1-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="b5da1-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="b5da1-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b5da1-296">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="b5da1-296">Performance and Tuning</span></span>
<span data-ttu-id="b5da1-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="b5da1-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
