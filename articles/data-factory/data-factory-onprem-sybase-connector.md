---
title: Move data from Sybase using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from Sybase Database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: jingwang
ms.openlocfilehash: cd0ccac4184f3e317d906ac9e2e16d179f5a13d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563505"
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="293f1-103">Move data from Sybase using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="293f1-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="293f1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span><span class="sxs-lookup"><span data-stu-id="293f1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="293f1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="293f1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="293f1-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="293f1-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="293f1-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="293f1-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="293f1-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span><span class="sxs-lookup"><span data-stu-id="293f1-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="293f1-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="293f1-109">Prerequisites</span></span>
<span data-ttu-id="293f1-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="293f1-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="293f1-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="293f1-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="293f1-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="293f1-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="293f1-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="293f1-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="293f1-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="293f1-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="293f1-115">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="293f1-115">Supported versions and installation</span></span>
<span data-ttu-id="293f1-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="293f1-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="293f1-117">Sybase version 16 and above is supported.</span><span class="sxs-lookup"><span data-stu-id="293f1-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="293f1-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="293f1-118">Getting started</span></span>
<span data-ttu-id="293f1-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="293f1-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="293f1-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="293f1-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="293f1-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="293f1-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="293f1-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="293f1-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="293f1-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="293f1-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="293f1-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="293f1-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="293f1-125">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="293f1-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="293f1-126">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="293f1-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="293f1-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="293f1-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="293f1-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="293f1-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="293f1-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="293f1-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="293f1-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="293f1-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="293f1-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span><span class="sxs-lookup"><span data-stu-id="293f1-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="293f1-132">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="293f1-132">Linked service properties</span></span>
<span data-ttu-id="293f1-133">The following table provides description for JSON elements specific to Sybase linked service.</span><span class="sxs-lookup"><span data-stu-id="293f1-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="293f1-134">Property</span><span class="sxs-lookup"><span data-stu-id="293f1-134">Property</span></span> | <span data-ttu-id="293f1-135">Description</span><span class="sxs-lookup"><span data-stu-id="293f1-135">Description</span></span> | <span data-ttu-id="293f1-136">Required</span><span class="sxs-lookup"><span data-stu-id="293f1-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="293f1-137">type</span><span class="sxs-lookup"><span data-stu-id="293f1-137">type</span></span> |<span data-ttu-id="293f1-138">The type property must be set to: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="293f1-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="293f1-139">Yes</span><span class="sxs-lookup"><span data-stu-id="293f1-139">Yes</span></span> |
| <span data-ttu-id="293f1-140">server</span><span class="sxs-lookup"><span data-stu-id="293f1-140">server</span></span> |<span data-ttu-id="293f1-141">Name of the Sybase server.</span><span class="sxs-lookup"><span data-stu-id="293f1-141">Name of the Sybase server.</span></span> |<span data-ttu-id="293f1-142">Yes</span><span class="sxs-lookup"><span data-stu-id="293f1-142">Yes</span></span> |
| <span data-ttu-id="293f1-143">database</span><span class="sxs-lookup"><span data-stu-id="293f1-143">database</span></span> |<span data-ttu-id="293f1-144">Name of the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="293f1-144">Name of the Sybase database.</span></span> |<span data-ttu-id="293f1-145">Yes</span><span class="sxs-lookup"><span data-stu-id="293f1-145">Yes</span></span> |
| <span data-ttu-id="293f1-146">schema</span><span class="sxs-lookup"><span data-stu-id="293f1-146">schema</span></span> |<span data-ttu-id="293f1-147">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="293f1-147">Name of the schema in the database.</span></span> |<span data-ttu-id="293f1-148">No</span><span class="sxs-lookup"><span data-stu-id="293f1-148">No</span></span> |
| <span data-ttu-id="293f1-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="293f1-149">authenticationType</span></span> |<span data-ttu-id="293f1-150">Type of authentication used to connect to the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="293f1-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="293f1-151">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="293f1-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="293f1-152">Yes</span><span class="sxs-lookup"><span data-stu-id="293f1-152">Yes</span></span> |
| <span data-ttu-id="293f1-153">username</span><span class="sxs-lookup"><span data-stu-id="293f1-153">username</span></span> |<span data-ttu-id="293f1-154">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="293f1-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="293f1-155">No</span><span class="sxs-lookup"><span data-stu-id="293f1-155">No</span></span> |
| <span data-ttu-id="293f1-156">password</span><span class="sxs-lookup"><span data-stu-id="293f1-156">password</span></span> |<span data-ttu-id="293f1-157">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="293f1-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="293f1-158">No</span><span class="sxs-lookup"><span data-stu-id="293f1-158">No</span></span> |
| <span data-ttu-id="293f1-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="293f1-159">gatewayName</span></span> |<span data-ttu-id="293f1-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span><span class="sxs-lookup"><span data-stu-id="293f1-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="293f1-161">Yes</span><span class="sxs-lookup"><span data-stu-id="293f1-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="293f1-162">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="293f1-162">Dataset properties</span></span>
<span data-ttu-id="293f1-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="293f1-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="293f1-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="293f1-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="293f1-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="293f1-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="293f1-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span><span class="sxs-lookup"><span data-stu-id="293f1-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="293f1-167">Property</span><span class="sxs-lookup"><span data-stu-id="293f1-167">Property</span></span> | <span data-ttu-id="293f1-168">Description</span><span class="sxs-lookup"><span data-stu-id="293f1-168">Description</span></span> | <span data-ttu-id="293f1-169">Required</span><span class="sxs-lookup"><span data-stu-id="293f1-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="293f1-170">tableName</span><span class="sxs-lookup"><span data-stu-id="293f1-170">tableName</span></span> |<span data-ttu-id="293f1-171">Name of the table in the Sybase Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="293f1-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="293f1-172">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="293f1-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="293f1-173">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="293f1-173">Copy activity properties</span></span>
<span data-ttu-id="293f1-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="293f1-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="293f1-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="293f1-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="293f1-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="293f1-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="293f1-177">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="293f1-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="293f1-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="293f1-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="293f1-179">Property</span><span class="sxs-lookup"><span data-stu-id="293f1-179">Property</span></span> | <span data-ttu-id="293f1-180">Description</span><span class="sxs-lookup"><span data-stu-id="293f1-180">Description</span></span> | <span data-ttu-id="293f1-181">Allowed values</span><span class="sxs-lookup"><span data-stu-id="293f1-181">Allowed values</span></span> | <span data-ttu-id="293f1-182">Required</span><span class="sxs-lookup"><span data-stu-id="293f1-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="293f1-183">query</span><span class="sxs-lookup"><span data-stu-id="293f1-183">query</span></span> |<span data-ttu-id="293f1-184">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="293f1-184">Use the custom query to read data.</span></span> |<span data-ttu-id="293f1-185">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="293f1-185">SQL query string.</span></span> <span data-ttu-id="293f1-186">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="293f1-186">For example: select \* from MyTable.</span></span> |<span data-ttu-id="293f1-187">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="293f1-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="293f1-188">JSON example: Copy data from Sybase to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="293f1-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="293f1-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="293f1-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="293f1-190">They show how to copy data from Sybase database to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="293f1-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="293f1-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="293f1-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="293f1-192">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="293f1-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="293f1-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="293f1-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="293f1-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="293f1-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="293f1-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="293f1-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="293f1-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="293f1-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="293f1-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="293f1-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="293f1-198">The sample copies data from a query result in Sybase database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="293f1-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="293f1-199">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="293f1-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="293f1-200">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="293f1-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="293f1-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="293f1-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="293f1-202">**Sybase linked service:**</span><span class="sxs-lookup"><span data-stu-id="293f1-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="293f1-203">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="293f1-203">**Azure Blob storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="293f1-204">**Sybase input dataset:**</span><span class="sxs-lookup"><span data-stu-id="293f1-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="293f1-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span><span class="sxs-lookup"><span data-stu-id="293f1-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="293f1-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="293f1-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="293f1-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="293f1-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
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

<span data-ttu-id="293f1-208">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="293f1-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="293f1-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="293f1-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="293f1-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="293f1-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="293f1-211">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="293f1-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="293f1-212">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="293f1-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="293f1-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span><span class="sxs-lookup"><span data-stu-id="293f1-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="293f1-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="293f1-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="293f1-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span><span class="sxs-lookup"><span data-stu-id="293f1-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="293f1-216">Type mapping for Sybase</span><span class="sxs-lookup"><span data-stu-id="293f1-216">Type mapping for Sybase</span></span>
<span data-ttu-id="293f1-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="293f1-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="293f1-218">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="293f1-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="293f1-219">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="293f1-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="293f1-220">Sybase supports T-SQL and T-SQL types.</span><span class="sxs-lookup"><span data-stu-id="293f1-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="293f1-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span><span class="sxs-lookup"><span data-stu-id="293f1-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="293f1-222">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="293f1-222">Map source to sink columns</span></span>
<span data-ttu-id="293f1-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="293f1-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="293f1-224">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="293f1-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="293f1-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="293f1-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="293f1-226">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="293f1-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="293f1-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="293f1-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="293f1-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="293f1-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="293f1-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="293f1-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="293f1-230">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="293f1-230">Performance and Tuning</span></span>
<span data-ttu-id="293f1-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="293f1-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
