---
title: Move data from Teradata using Azure Data Factory | Microsoft Docs
description: Learn about Teradata Connector for the Data Factory service that lets you move data from Teradata Database
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: ee2440171b54e1279571ec4fcb0c5be7bec207a1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867472"
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="937f7-103">Move data from Teradata using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="937f7-103">Move data from Teradata using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-onprem-teradata-connector.md)
> * [Version 2 (current version)](../connector-teradata.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Teradata connector in V2](../connector-teradata.md).

<span data-ttu-id="937f7-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span><span class="sxs-lookup"><span data-stu-id="937f7-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="937f7-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="937f7-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="937f7-110">You can copy data from an on-premises Teradata data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="937f7-110">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="937f7-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="937f7-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="937f7-112">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span><span class="sxs-lookup"><span data-stu-id="937f7-112">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="937f7-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="937f7-113">Prerequisites</span></span>
<span data-ttu-id="937f7-114">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="937f7-114">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="937f7-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="937f7-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="937f7-116">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="937f7-116">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="937f7-117">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="937f7-117">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.

## <a name="supported-versions-and-installation"></a><span data-ttu-id="937f7-119">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="937f7-119">Supported versions and installation</span></span>
<span data-ttu-id="937f7-120">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="937f7-120">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="937f7-121">Teradata version 12 and above is supported.</span><span class="sxs-lookup"><span data-stu-id="937f7-121">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="937f7-122">Getting started</span><span class="sxs-lookup"><span data-stu-id="937f7-122">Getting started</span></span>
<span data-ttu-id="937f7-123">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="937f7-123">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="937f7-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="937f7-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="937f7-125">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="937f7-125">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="937f7-126">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="937f7-126">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="937f7-127">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="937f7-127">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="937f7-128">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="937f7-128">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="937f7-129">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="937f7-129">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="937f7-130">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="937f7-130">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="937f7-131">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="937f7-131">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="937f7-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="937f7-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="937f7-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="937f7-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="937f7-134">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="937f7-134">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="937f7-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span><span class="sxs-lookup"><span data-stu-id="937f7-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="937f7-136">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="937f7-136">Linked service properties</span></span>
<span data-ttu-id="937f7-137">The following table provides description for JSON elements specific to Teradata linked service.</span><span class="sxs-lookup"><span data-stu-id="937f7-137">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="937f7-138">Property</span><span class="sxs-lookup"><span data-stu-id="937f7-138">Property</span></span> | <span data-ttu-id="937f7-139">Description</span><span class="sxs-lookup"><span data-stu-id="937f7-139">Description</span></span> | <span data-ttu-id="937f7-140">Required</span><span class="sxs-lookup"><span data-stu-id="937f7-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="937f7-141">type</span><span class="sxs-lookup"><span data-stu-id="937f7-141">type</span></span> |<span data-ttu-id="937f7-142">The type property must be set to: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="937f7-142">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="937f7-143">Yes</span><span class="sxs-lookup"><span data-stu-id="937f7-143">Yes</span></span> |
| <span data-ttu-id="937f7-144">server</span><span class="sxs-lookup"><span data-stu-id="937f7-144">server</span></span> |<span data-ttu-id="937f7-145">Name of the Teradata server.</span><span class="sxs-lookup"><span data-stu-id="937f7-145">Name of the Teradata server.</span></span> |<span data-ttu-id="937f7-146">Yes</span><span class="sxs-lookup"><span data-stu-id="937f7-146">Yes</span></span> |
| <span data-ttu-id="937f7-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="937f7-147">authenticationType</span></span> |<span data-ttu-id="937f7-148">Type of authentication used to connect to the Teradata database.</span><span class="sxs-lookup"><span data-stu-id="937f7-148">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="937f7-149">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="937f7-149">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="937f7-150">Yes</span><span class="sxs-lookup"><span data-stu-id="937f7-150">Yes</span></span> |
| <span data-ttu-id="937f7-151">username</span><span class="sxs-lookup"><span data-stu-id="937f7-151">username</span></span> |<span data-ttu-id="937f7-152">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="937f7-152">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="937f7-153">No</span><span class="sxs-lookup"><span data-stu-id="937f7-153">No</span></span> |
| <span data-ttu-id="937f7-154">password</span><span class="sxs-lookup"><span data-stu-id="937f7-154">password</span></span> |<span data-ttu-id="937f7-155">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="937f7-155">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="937f7-156">No</span><span class="sxs-lookup"><span data-stu-id="937f7-156">No</span></span> |
| <span data-ttu-id="937f7-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="937f7-157">gatewayName</span></span> |<span data-ttu-id="937f7-158">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span><span class="sxs-lookup"><span data-stu-id="937f7-158">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="937f7-159">Yes</span><span class="sxs-lookup"><span data-stu-id="937f7-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="937f7-160">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="937f7-160">Dataset properties</span></span>
<span data-ttu-id="937f7-161">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="937f7-161">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="937f7-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="937f7-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="937f7-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="937f7-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="937f7-164">Currently, there are no type properties supported for the Teradata dataset.</span><span class="sxs-lookup"><span data-stu-id="937f7-164">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="937f7-165">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="937f7-165">Copy activity properties</span></span>
<span data-ttu-id="937f7-166">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="937f7-166">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="937f7-167">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="937f7-167">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="937f7-168">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="937f7-168">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="937f7-169">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="937f7-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="937f7-170">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="937f7-170">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="937f7-171">Property</span><span class="sxs-lookup"><span data-stu-id="937f7-171">Property</span></span> | <span data-ttu-id="937f7-172">Description</span><span class="sxs-lookup"><span data-stu-id="937f7-172">Description</span></span> | <span data-ttu-id="937f7-173">Allowed values</span><span class="sxs-lookup"><span data-stu-id="937f7-173">Allowed values</span></span> | <span data-ttu-id="937f7-174">Required</span><span class="sxs-lookup"><span data-stu-id="937f7-174">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="937f7-175">query</span><span class="sxs-lookup"><span data-stu-id="937f7-175">query</span></span> |<span data-ttu-id="937f7-176">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="937f7-176">Use the custom query to read data.</span></span> |<span data-ttu-id="937f7-177">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="937f7-177">SQL query string.</span></span> <span data-ttu-id="937f7-178">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="937f7-178">For example: select \* from MyTable.</span></span> |<span data-ttu-id="937f7-179">Yes</span><span class="sxs-lookup"><span data-stu-id="937f7-179">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="937f7-180">JSON example: Copy data from Teradata to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="937f7-180">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="937f7-181">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="937f7-181">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="937f7-182">They show how to copy data from Teradata to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="937f7-182">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="937f7-183">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="937f7-183">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="937f7-184">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="937f7-184">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="937f7-185">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="937f7-185">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="937f7-186">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="937f7-186">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="937f7-187">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="937f7-187">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="937f7-188">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="937f7-188">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="937f7-189">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="937f7-189">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="937f7-190">The sample copies data from a query result in Teradata database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="937f7-190">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="937f7-191">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="937f7-191">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="937f7-192">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="937f7-192">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="937f7-193">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="937f7-193">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="937f7-194">**Teradata linked service:**</span><span class="sxs-lookup"><span data-stu-id="937f7-194">**Teradata linked service:**</span></span>

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

<span data-ttu-id="937f7-195">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="937f7-195">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="937f7-196">**Teradata input dataset:**</span><span class="sxs-lookup"><span data-stu-id="937f7-196">**Teradata input dataset:**</span></span>

<span data-ttu-id="937f7-197">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span><span class="sxs-lookup"><span data-stu-id="937f7-197">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="937f7-198">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="937f7-198">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="937f7-199">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="937f7-199">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="937f7-200">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="937f7-200">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="937f7-201">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="937f7-201">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="937f7-202">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="937f7-202">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="937f7-203">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="937f7-203">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="937f7-204">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span><span class="sxs-lookup"><span data-stu-id="937f7-204">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="937f7-205">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="937f7-205">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="937f7-206">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="937f7-206">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="937f7-207">Type mapping for Teradata</span><span class="sxs-lookup"><span data-stu-id="937f7-207">Type mapping for Teradata</span></span>
<span data-ttu-id="937f7-208">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="937f7-208">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="937f7-209">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="937f7-209">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="937f7-210">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="937f7-210">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="937f7-211">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span><span class="sxs-lookup"><span data-stu-id="937f7-211">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="937f7-212">Teradata Database type</span><span class="sxs-lookup"><span data-stu-id="937f7-212">Teradata Database type</span></span> | <span data-ttu-id="937f7-213">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="937f7-213">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="937f7-214">Char</span><span class="sxs-lookup"><span data-stu-id="937f7-214">Char</span></span> |<span data-ttu-id="937f7-215">String</span><span class="sxs-lookup"><span data-stu-id="937f7-215">String</span></span> |
| <span data-ttu-id="937f7-216">Clob</span><span class="sxs-lookup"><span data-stu-id="937f7-216">Clob</span></span> |<span data-ttu-id="937f7-217">String</span><span class="sxs-lookup"><span data-stu-id="937f7-217">String</span></span> |
| <span data-ttu-id="937f7-218">Graphic</span><span class="sxs-lookup"><span data-stu-id="937f7-218">Graphic</span></span> |<span data-ttu-id="937f7-219">String</span><span class="sxs-lookup"><span data-stu-id="937f7-219">String</span></span> |
| <span data-ttu-id="937f7-220">VarChar</span><span class="sxs-lookup"><span data-stu-id="937f7-220">VarChar</span></span> |<span data-ttu-id="937f7-221">String</span><span class="sxs-lookup"><span data-stu-id="937f7-221">String</span></span> |
| <span data-ttu-id="937f7-222">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="937f7-222">VarGraphic</span></span> |<span data-ttu-id="937f7-223">String</span><span class="sxs-lookup"><span data-stu-id="937f7-223">String</span></span> |
| <span data-ttu-id="937f7-224">Blob</span><span class="sxs-lookup"><span data-stu-id="937f7-224">Blob</span></span> |<span data-ttu-id="937f7-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="937f7-225">Byte[]</span></span> |
| <span data-ttu-id="937f7-226">Byte</span><span class="sxs-lookup"><span data-stu-id="937f7-226">Byte</span></span> |<span data-ttu-id="937f7-227">Byte[]</span><span class="sxs-lookup"><span data-stu-id="937f7-227">Byte[]</span></span> |
| <span data-ttu-id="937f7-228">VarByte</span><span class="sxs-lookup"><span data-stu-id="937f7-228">VarByte</span></span> |<span data-ttu-id="937f7-229">Byte[]</span><span class="sxs-lookup"><span data-stu-id="937f7-229">Byte[]</span></span> |
| <span data-ttu-id="937f7-230">BigInt</span><span class="sxs-lookup"><span data-stu-id="937f7-230">BigInt</span></span> |<span data-ttu-id="937f7-231">Int64</span><span class="sxs-lookup"><span data-stu-id="937f7-231">Int64</span></span> |
| <span data-ttu-id="937f7-232">ByteInt</span><span class="sxs-lookup"><span data-stu-id="937f7-232">ByteInt</span></span> |<span data-ttu-id="937f7-233">Int16</span><span class="sxs-lookup"><span data-stu-id="937f7-233">Int16</span></span> |
| <span data-ttu-id="937f7-234">Decimal</span><span class="sxs-lookup"><span data-stu-id="937f7-234">Decimal</span></span> |<span data-ttu-id="937f7-235">Decimal</span><span class="sxs-lookup"><span data-stu-id="937f7-235">Decimal</span></span> |
| <span data-ttu-id="937f7-236">Double</span><span class="sxs-lookup"><span data-stu-id="937f7-236">Double</span></span> |<span data-ttu-id="937f7-237">Double</span><span class="sxs-lookup"><span data-stu-id="937f7-237">Double</span></span> |
| <span data-ttu-id="937f7-238">Integer</span><span class="sxs-lookup"><span data-stu-id="937f7-238">Integer</span></span> |<span data-ttu-id="937f7-239">Int32</span><span class="sxs-lookup"><span data-stu-id="937f7-239">Int32</span></span> |
| <span data-ttu-id="937f7-240">Number</span><span class="sxs-lookup"><span data-stu-id="937f7-240">Number</span></span> |<span data-ttu-id="937f7-241">Double</span><span class="sxs-lookup"><span data-stu-id="937f7-241">Double</span></span> |
| <span data-ttu-id="937f7-242">SmallInt</span><span class="sxs-lookup"><span data-stu-id="937f7-242">SmallInt</span></span> |<span data-ttu-id="937f7-243">Int16</span><span class="sxs-lookup"><span data-stu-id="937f7-243">Int16</span></span> |
| <span data-ttu-id="937f7-244">Date</span><span class="sxs-lookup"><span data-stu-id="937f7-244">Date</span></span> |<span data-ttu-id="937f7-245">DateTime</span><span class="sxs-lookup"><span data-stu-id="937f7-245">DateTime</span></span> |
| <span data-ttu-id="937f7-246">Time</span><span class="sxs-lookup"><span data-stu-id="937f7-246">Time</span></span> |<span data-ttu-id="937f7-247">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-247">TimeSpan</span></span> |
| <span data-ttu-id="937f7-248">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="937f7-248">Time With Time Zone</span></span> |<span data-ttu-id="937f7-249">String</span><span class="sxs-lookup"><span data-stu-id="937f7-249">String</span></span> |
| <span data-ttu-id="937f7-250">Timestamp</span><span class="sxs-lookup"><span data-stu-id="937f7-250">Timestamp</span></span> |<span data-ttu-id="937f7-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="937f7-251">DateTime</span></span> |
| <span data-ttu-id="937f7-252">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="937f7-252">Timestamp With Time Zone</span></span> |<span data-ttu-id="937f7-253">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="937f7-253">DateTimeOffset</span></span> |
| <span data-ttu-id="937f7-254">Interval Day</span><span class="sxs-lookup"><span data-stu-id="937f7-254">Interval Day</span></span> |<span data-ttu-id="937f7-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-255">TimeSpan</span></span> |
| <span data-ttu-id="937f7-256">Interval Day To Hour</span><span class="sxs-lookup"><span data-stu-id="937f7-256">Interval Day To Hour</span></span> |<span data-ttu-id="937f7-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-257">TimeSpan</span></span> |
| <span data-ttu-id="937f7-258">Interval Day To Minute</span><span class="sxs-lookup"><span data-stu-id="937f7-258">Interval Day To Minute</span></span> |<span data-ttu-id="937f7-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-259">TimeSpan</span></span> |
| <span data-ttu-id="937f7-260">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="937f7-260">Interval Day To Second</span></span> |<span data-ttu-id="937f7-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-261">TimeSpan</span></span> |
| <span data-ttu-id="937f7-262">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="937f7-262">Interval Hour</span></span> |<span data-ttu-id="937f7-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-263">TimeSpan</span></span> |
| <span data-ttu-id="937f7-264">Interval Hour To Minute</span><span class="sxs-lookup"><span data-stu-id="937f7-264">Interval Hour To Minute</span></span> |<span data-ttu-id="937f7-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-265">TimeSpan</span></span> |
| <span data-ttu-id="937f7-266">Interval Hour To Second</span><span class="sxs-lookup"><span data-stu-id="937f7-266">Interval Hour To Second</span></span> |<span data-ttu-id="937f7-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-267">TimeSpan</span></span> |
| <span data-ttu-id="937f7-268">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="937f7-268">Interval Minute</span></span> |<span data-ttu-id="937f7-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-269">TimeSpan</span></span> |
| <span data-ttu-id="937f7-270">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="937f7-270">Interval Minute To Second</span></span> |<span data-ttu-id="937f7-271">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-271">TimeSpan</span></span> |
| <span data-ttu-id="937f7-272">Interval Second</span><span class="sxs-lookup"><span data-stu-id="937f7-272">Interval Second</span></span> |<span data-ttu-id="937f7-273">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="937f7-273">TimeSpan</span></span> |
| <span data-ttu-id="937f7-274">Interval Year</span><span class="sxs-lookup"><span data-stu-id="937f7-274">Interval Year</span></span> |<span data-ttu-id="937f7-275">String</span><span class="sxs-lookup"><span data-stu-id="937f7-275">String</span></span> |
| <span data-ttu-id="937f7-276">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="937f7-276">Interval Year To Month</span></span> |<span data-ttu-id="937f7-277">String</span><span class="sxs-lookup"><span data-stu-id="937f7-277">String</span></span> |
| <span data-ttu-id="937f7-278">Interval Month</span><span class="sxs-lookup"><span data-stu-id="937f7-278">Interval Month</span></span> |<span data-ttu-id="937f7-279">String</span><span class="sxs-lookup"><span data-stu-id="937f7-279">String</span></span> |
| <span data-ttu-id="937f7-280">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="937f7-280">Period(Date)</span></span> |<span data-ttu-id="937f7-281">String</span><span class="sxs-lookup"><span data-stu-id="937f7-281">String</span></span> |
| <span data-ttu-id="937f7-282">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="937f7-282">Period(Time)</span></span> |<span data-ttu-id="937f7-283">String</span><span class="sxs-lookup"><span data-stu-id="937f7-283">String</span></span> |
| <span data-ttu-id="937f7-284">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="937f7-284">Period(Time With Time Zone)</span></span> |<span data-ttu-id="937f7-285">String</span><span class="sxs-lookup"><span data-stu-id="937f7-285">String</span></span> |
| <span data-ttu-id="937f7-286">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="937f7-286">Period(Timestamp)</span></span> |<span data-ttu-id="937f7-287">String</span><span class="sxs-lookup"><span data-stu-id="937f7-287">String</span></span> |
| <span data-ttu-id="937f7-288">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="937f7-288">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="937f7-289">String</span><span class="sxs-lookup"><span data-stu-id="937f7-289">String</span></span> |
| <span data-ttu-id="937f7-290">Xml</span><span class="sxs-lookup"><span data-stu-id="937f7-290">Xml</span></span> |<span data-ttu-id="937f7-291">String</span><span class="sxs-lookup"><span data-stu-id="937f7-291">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="937f7-292">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="937f7-292">Map source to sink columns</span></span>
<span data-ttu-id="937f7-293">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="937f7-293">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="937f7-294">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="937f7-294">Repeatable read from relational sources</span></span>
<span data-ttu-id="937f7-295">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="937f7-295">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="937f7-296">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="937f7-296">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="937f7-297">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="937f7-297">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="937f7-298">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="937f7-298">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="937f7-299">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="937f7-299">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="937f7-300">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="937f7-300">Performance and Tuning</span></span>
<span data-ttu-id="937f7-301">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="937f7-301">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
