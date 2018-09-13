---
title: Move data from MySQL using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from MySQL database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: jingwang
ms.openlocfilehash: 6320331adc80998f1f64cdfa56839d940708bdc4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552183"
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="ff011-103">Move data From MySQL using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ff011-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="ff011-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span><span class="sxs-lookup"><span data-stu-id="ff011-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="ff011-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="ff011-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="ff011-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="ff011-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="ff011-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="ff011-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ff011-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span><span class="sxs-lookup"><span data-stu-id="ff011-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ff011-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff011-109">Prerequisites</span></span>
<span data-ttu-id="ff011-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="ff011-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="ff011-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="ff011-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="ff011-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="ff011-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="ff011-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="ff011-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="ff011-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="ff011-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="ff011-115">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="ff011-115">Supported versions and installation</span></span>
<span data-ttu-id="ff011-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net 6.6.5 for Microsoft Windows](http://go.microsoft.com/fwlink/?LinkId=278885) or above on the same system as the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="ff011-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net 6.6.5 for Microsoft Windows](http://go.microsoft.com/fwlink/?LinkId=278885) or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="ff011-117">MySQL version 5.1 and above is supported.</span><span class="sxs-lookup"><span data-stu-id="ff011-117">MySQL version 5.1 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ff011-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="ff011-118">Getting started</span></span>
<span data-ttu-id="ff011-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="ff011-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="ff011-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="ff011-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="ff011-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="ff011-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="ff011-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="ff011-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ff011-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="ff011-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ff011-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="ff011-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="ff011-125">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="ff011-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="ff011-126">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="ff011-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="ff011-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="ff011-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ff011-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="ff011-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="ff011-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="ff011-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="ff011-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="ff011-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="ff011-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span><span class="sxs-lookup"><span data-stu-id="ff011-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ff011-132">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="ff011-132">Linked service properties</span></span>
<span data-ttu-id="ff011-133">The following table provides description for JSON elements specific to MySQL linked service.</span><span class="sxs-lookup"><span data-stu-id="ff011-133">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="ff011-134">Property</span><span class="sxs-lookup"><span data-stu-id="ff011-134">Property</span></span> | <span data-ttu-id="ff011-135">Description</span><span class="sxs-lookup"><span data-stu-id="ff011-135">Description</span></span> | <span data-ttu-id="ff011-136">Required</span><span class="sxs-lookup"><span data-stu-id="ff011-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff011-137">type</span><span class="sxs-lookup"><span data-stu-id="ff011-137">type</span></span> |<span data-ttu-id="ff011-138">The type property must be set to: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="ff011-138">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="ff011-139">Yes</span><span class="sxs-lookup"><span data-stu-id="ff011-139">Yes</span></span> |
| <span data-ttu-id="ff011-140">server</span><span class="sxs-lookup"><span data-stu-id="ff011-140">server</span></span> |<span data-ttu-id="ff011-141">Name of the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="ff011-141">Name of the MySQL server.</span></span> |<span data-ttu-id="ff011-142">Yes</span><span class="sxs-lookup"><span data-stu-id="ff011-142">Yes</span></span> |
| <span data-ttu-id="ff011-143">database</span><span class="sxs-lookup"><span data-stu-id="ff011-143">database</span></span> |<span data-ttu-id="ff011-144">Name of the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="ff011-144">Name of the MySQL database.</span></span> |<span data-ttu-id="ff011-145">Yes</span><span class="sxs-lookup"><span data-stu-id="ff011-145">Yes</span></span> |
| <span data-ttu-id="ff011-146">schema</span><span class="sxs-lookup"><span data-stu-id="ff011-146">schema</span></span> |<span data-ttu-id="ff011-147">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="ff011-147">Name of the schema in the database.</span></span> |<span data-ttu-id="ff011-148">No</span><span class="sxs-lookup"><span data-stu-id="ff011-148">No</span></span> |
| <span data-ttu-id="ff011-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ff011-149">authenticationType</span></span> |<span data-ttu-id="ff011-150">Type of authentication used to connect to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="ff011-150">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="ff011-151">Possible values are: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="ff011-151">Possible values are: `Basic`.</span></span> |<span data-ttu-id="ff011-152">Yes</span><span class="sxs-lookup"><span data-stu-id="ff011-152">Yes</span></span> |
| <span data-ttu-id="ff011-153">username</span><span class="sxs-lookup"><span data-stu-id="ff011-153">username</span></span> |<span data-ttu-id="ff011-154">Specify user name to connect to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="ff011-154">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="ff011-155">Yes</span><span class="sxs-lookup"><span data-stu-id="ff011-155">Yes</span></span> |
| <span data-ttu-id="ff011-156">password</span><span class="sxs-lookup"><span data-stu-id="ff011-156">password</span></span> |<span data-ttu-id="ff011-157">Specify password for the user account you specified.</span><span class="sxs-lookup"><span data-stu-id="ff011-157">Specify password for the user account you specified.</span></span> |<span data-ttu-id="ff011-158">Yes</span><span class="sxs-lookup"><span data-stu-id="ff011-158">Yes</span></span> |
| <span data-ttu-id="ff011-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ff011-159">gatewayName</span></span> |<span data-ttu-id="ff011-160">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span><span class="sxs-lookup"><span data-stu-id="ff011-160">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="ff011-161">Yes</span><span class="sxs-lookup"><span data-stu-id="ff011-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="ff011-162">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="ff011-162">Dataset properties</span></span>
<span data-ttu-id="ff011-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="ff011-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ff011-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="ff011-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ff011-165">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="ff011-165">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="ff011-166">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span><span class="sxs-lookup"><span data-stu-id="ff011-166">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="ff011-167">Property</span><span class="sxs-lookup"><span data-stu-id="ff011-167">Property</span></span> | <span data-ttu-id="ff011-168">Description</span><span class="sxs-lookup"><span data-stu-id="ff011-168">Description</span></span> | <span data-ttu-id="ff011-169">Required</span><span class="sxs-lookup"><span data-stu-id="ff011-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff011-170">tableName</span><span class="sxs-lookup"><span data-stu-id="ff011-170">tableName</span></span> |<span data-ttu-id="ff011-171">Name of the table in the MySQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="ff011-171">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="ff011-172">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="ff011-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ff011-173">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="ff011-173">Copy activity properties</span></span>
<span data-ttu-id="ff011-174">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="ff011-174">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ff011-175">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="ff011-175">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="ff011-176">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="ff011-176">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="ff011-177">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="ff011-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="ff011-178">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="ff011-178">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="ff011-179">Property</span><span class="sxs-lookup"><span data-stu-id="ff011-179">Property</span></span> | <span data-ttu-id="ff011-180">Description</span><span class="sxs-lookup"><span data-stu-id="ff011-180">Description</span></span> | <span data-ttu-id="ff011-181">Allowed values</span><span class="sxs-lookup"><span data-stu-id="ff011-181">Allowed values</span></span> | <span data-ttu-id="ff011-182">Required</span><span class="sxs-lookup"><span data-stu-id="ff011-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ff011-183">query</span><span class="sxs-lookup"><span data-stu-id="ff011-183">query</span></span> |<span data-ttu-id="ff011-184">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="ff011-184">Use the custom query to read data.</span></span> |<span data-ttu-id="ff011-185">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="ff011-185">SQL query string.</span></span> <span data-ttu-id="ff011-186">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="ff011-186">For example: select \* from MyTable.</span></span> |<span data-ttu-id="ff011-187">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="ff011-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="ff011-188">JSON example: Copy data from MySQL to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="ff011-188">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="ff011-189">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ff011-189">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ff011-190">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ff011-190">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="ff011-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ff011-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff011-192">This sample provides JSON snippets.</span><span class="sxs-lookup"><span data-stu-id="ff011-192">This sample provides JSON snippets.</span></span> <span data-ttu-id="ff011-193">It does not include step-by-step instructions for creating the data factory.</span><span class="sxs-lookup"><span data-stu-id="ff011-193">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="ff011-194">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="ff011-194">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="ff011-195">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="ff011-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="ff011-196">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ff011-196">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="ff011-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ff011-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ff011-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ff011-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ff011-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ff011-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ff011-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ff011-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ff011-201">The sample copies data from a query result in MySQL database to a blob hourly.</span><span class="sxs-lookup"><span data-stu-id="ff011-201">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="ff011-202">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="ff011-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ff011-203">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="ff011-203">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="ff011-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="ff011-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="ff011-205">**MySQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="ff011-205">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="ff011-206">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="ff011-206">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="ff011-207">**MySQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="ff011-207">**MySQL input dataset:**</span></span>

<span data-ttu-id="ff011-208">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="ff011-208">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="ff011-209">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="ff011-209">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
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

<span data-ttu-id="ff011-210">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="ff011-210">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ff011-211">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="ff011-211">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ff011-212">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="ff011-212">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ff011-213">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="ff011-213">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="ff011-214">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="ff011-214">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="ff011-215">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="ff011-215">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ff011-216">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ff011-216">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="ff011-217">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="ff011-217">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
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
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="ff011-218">Type mapping for MySQL</span><span class="sxs-lookup"><span data-stu-id="ff011-218">Type mapping for MySQL</span></span>
<span data-ttu-id="ff011-219">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span><span class="sxs-lookup"><span data-stu-id="ff011-219">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="ff011-220">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="ff011-220">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="ff011-221">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="ff011-221">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="ff011-222">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span><span class="sxs-lookup"><span data-stu-id="ff011-222">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="ff011-223">MySQL Database type</span><span class="sxs-lookup"><span data-stu-id="ff011-223">MySQL Database type</span></span> | <span data-ttu-id="ff011-224">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="ff011-224">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="ff011-225">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="ff011-225">bigint unsigned</span></span> |<span data-ttu-id="ff011-226">Decimal</span><span class="sxs-lookup"><span data-stu-id="ff011-226">Decimal</span></span> |
| <span data-ttu-id="ff011-227">bigint</span><span class="sxs-lookup"><span data-stu-id="ff011-227">bigint</span></span> |<span data-ttu-id="ff011-228">Int64</span><span class="sxs-lookup"><span data-stu-id="ff011-228">Int64</span></span> |
| <span data-ttu-id="ff011-229">bit</span><span class="sxs-lookup"><span data-stu-id="ff011-229">bit</span></span> |<span data-ttu-id="ff011-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="ff011-230">Decimal</span></span> |
| <span data-ttu-id="ff011-231">blob</span><span class="sxs-lookup"><span data-stu-id="ff011-231">blob</span></span> |<span data-ttu-id="ff011-232">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ff011-232">Byte[]</span></span> |
| <span data-ttu-id="ff011-233">bool</span><span class="sxs-lookup"><span data-stu-id="ff011-233">bool</span></span> |<span data-ttu-id="ff011-234">Boolean</span><span class="sxs-lookup"><span data-stu-id="ff011-234">Boolean</span></span> |
| <span data-ttu-id="ff011-235">char</span><span class="sxs-lookup"><span data-stu-id="ff011-235">char</span></span> |<span data-ttu-id="ff011-236">String</span><span class="sxs-lookup"><span data-stu-id="ff011-236">String</span></span> |
| <span data-ttu-id="ff011-237">date</span><span class="sxs-lookup"><span data-stu-id="ff011-237">date</span></span> |<span data-ttu-id="ff011-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="ff011-238">Datetime</span></span> |
| <span data-ttu-id="ff011-239">datetime</span><span class="sxs-lookup"><span data-stu-id="ff011-239">datetime</span></span> |<span data-ttu-id="ff011-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="ff011-240">Datetime</span></span> |
| <span data-ttu-id="ff011-241">decimal</span><span class="sxs-lookup"><span data-stu-id="ff011-241">decimal</span></span> |<span data-ttu-id="ff011-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="ff011-242">Decimal</span></span> |
| <span data-ttu-id="ff011-243">double precision</span><span class="sxs-lookup"><span data-stu-id="ff011-243">double precision</span></span> |<span data-ttu-id="ff011-244">Double</span><span class="sxs-lookup"><span data-stu-id="ff011-244">Double</span></span> |
| <span data-ttu-id="ff011-245">double</span><span class="sxs-lookup"><span data-stu-id="ff011-245">double</span></span> |<span data-ttu-id="ff011-246">Double</span><span class="sxs-lookup"><span data-stu-id="ff011-246">Double</span></span> |
| <span data-ttu-id="ff011-247">enum</span><span class="sxs-lookup"><span data-stu-id="ff011-247">enum</span></span> |<span data-ttu-id="ff011-248">String</span><span class="sxs-lookup"><span data-stu-id="ff011-248">String</span></span> |
| <span data-ttu-id="ff011-249">float</span><span class="sxs-lookup"><span data-stu-id="ff011-249">float</span></span> |<span data-ttu-id="ff011-250">Single</span><span class="sxs-lookup"><span data-stu-id="ff011-250">Single</span></span> |
| <span data-ttu-id="ff011-251">int unsigned</span><span class="sxs-lookup"><span data-stu-id="ff011-251">int unsigned</span></span> |<span data-ttu-id="ff011-252">Int64</span><span class="sxs-lookup"><span data-stu-id="ff011-252">Int64</span></span> |
| <span data-ttu-id="ff011-253">int</span><span class="sxs-lookup"><span data-stu-id="ff011-253">int</span></span> |<span data-ttu-id="ff011-254">Int32</span><span class="sxs-lookup"><span data-stu-id="ff011-254">Int32</span></span> |
| <span data-ttu-id="ff011-255">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="ff011-255">integer unsigned</span></span> |<span data-ttu-id="ff011-256">Int64</span><span class="sxs-lookup"><span data-stu-id="ff011-256">Int64</span></span> |
| <span data-ttu-id="ff011-257">integer</span><span class="sxs-lookup"><span data-stu-id="ff011-257">integer</span></span> |<span data-ttu-id="ff011-258">Int32</span><span class="sxs-lookup"><span data-stu-id="ff011-258">Int32</span></span> |
| <span data-ttu-id="ff011-259">long varbinary</span><span class="sxs-lookup"><span data-stu-id="ff011-259">long varbinary</span></span> |<span data-ttu-id="ff011-260">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ff011-260">Byte[]</span></span> |
| <span data-ttu-id="ff011-261">long varchar</span><span class="sxs-lookup"><span data-stu-id="ff011-261">long varchar</span></span> |<span data-ttu-id="ff011-262">String</span><span class="sxs-lookup"><span data-stu-id="ff011-262">String</span></span> |
| <span data-ttu-id="ff011-263">longblob</span><span class="sxs-lookup"><span data-stu-id="ff011-263">longblob</span></span> |<span data-ttu-id="ff011-264">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ff011-264">Byte[]</span></span> |
| <span data-ttu-id="ff011-265">longtext</span><span class="sxs-lookup"><span data-stu-id="ff011-265">longtext</span></span> |<span data-ttu-id="ff011-266">String</span><span class="sxs-lookup"><span data-stu-id="ff011-266">String</span></span> |
| <span data-ttu-id="ff011-267">mediumblob</span><span class="sxs-lookup"><span data-stu-id="ff011-267">mediumblob</span></span> |<span data-ttu-id="ff011-268">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ff011-268">Byte[]</span></span> |
| <span data-ttu-id="ff011-269">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="ff011-269">mediumint unsigned</span></span> |<span data-ttu-id="ff011-270">Int64</span><span class="sxs-lookup"><span data-stu-id="ff011-270">Int64</span></span> |
| <span data-ttu-id="ff011-271">mediumint</span><span class="sxs-lookup"><span data-stu-id="ff011-271">mediumint</span></span> |<span data-ttu-id="ff011-272">Int32</span><span class="sxs-lookup"><span data-stu-id="ff011-272">Int32</span></span> |
| <span data-ttu-id="ff011-273">mediumtext</span><span class="sxs-lookup"><span data-stu-id="ff011-273">mediumtext</span></span> |<span data-ttu-id="ff011-274">String</span><span class="sxs-lookup"><span data-stu-id="ff011-274">String</span></span> |
| <span data-ttu-id="ff011-275">numeric</span><span class="sxs-lookup"><span data-stu-id="ff011-275">numeric</span></span> |<span data-ttu-id="ff011-276">Decimal</span><span class="sxs-lookup"><span data-stu-id="ff011-276">Decimal</span></span> |
| <span data-ttu-id="ff011-277">real</span><span class="sxs-lookup"><span data-stu-id="ff011-277">real</span></span> |<span data-ttu-id="ff011-278">Double</span><span class="sxs-lookup"><span data-stu-id="ff011-278">Double</span></span> |
| <span data-ttu-id="ff011-279">set</span><span class="sxs-lookup"><span data-stu-id="ff011-279">set</span></span> |<span data-ttu-id="ff011-280">String</span><span class="sxs-lookup"><span data-stu-id="ff011-280">String</span></span> |
| <span data-ttu-id="ff011-281">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="ff011-281">smallint unsigned</span></span> |<span data-ttu-id="ff011-282">Int32</span><span class="sxs-lookup"><span data-stu-id="ff011-282">Int32</span></span> |
| <span data-ttu-id="ff011-283">smallint</span><span class="sxs-lookup"><span data-stu-id="ff011-283">smallint</span></span> |<span data-ttu-id="ff011-284">Int16</span><span class="sxs-lookup"><span data-stu-id="ff011-284">Int16</span></span> |
| <span data-ttu-id="ff011-285">text</span><span class="sxs-lookup"><span data-stu-id="ff011-285">text</span></span> |<span data-ttu-id="ff011-286">String</span><span class="sxs-lookup"><span data-stu-id="ff011-286">String</span></span> |
| <span data-ttu-id="ff011-287">time</span><span class="sxs-lookup"><span data-stu-id="ff011-287">time</span></span> |<span data-ttu-id="ff011-288">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ff011-288">TimeSpan</span></span> |
| <span data-ttu-id="ff011-289">timestamp</span><span class="sxs-lookup"><span data-stu-id="ff011-289">timestamp</span></span> |<span data-ttu-id="ff011-290">Datetime</span><span class="sxs-lookup"><span data-stu-id="ff011-290">Datetime</span></span> |
| <span data-ttu-id="ff011-291">tinyblob</span><span class="sxs-lookup"><span data-stu-id="ff011-291">tinyblob</span></span> |<span data-ttu-id="ff011-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ff011-292">Byte[]</span></span> |
| <span data-ttu-id="ff011-293">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="ff011-293">tinyint unsigned</span></span> |<span data-ttu-id="ff011-294">Int16</span><span class="sxs-lookup"><span data-stu-id="ff011-294">Int16</span></span> |
| <span data-ttu-id="ff011-295">tinyint</span><span class="sxs-lookup"><span data-stu-id="ff011-295">tinyint</span></span> |<span data-ttu-id="ff011-296">Int16</span><span class="sxs-lookup"><span data-stu-id="ff011-296">Int16</span></span> |
| <span data-ttu-id="ff011-297">tinytext</span><span class="sxs-lookup"><span data-stu-id="ff011-297">tinytext</span></span> |<span data-ttu-id="ff011-298">String</span><span class="sxs-lookup"><span data-stu-id="ff011-298">String</span></span> |
| <span data-ttu-id="ff011-299">varchar</span><span class="sxs-lookup"><span data-stu-id="ff011-299">varchar</span></span> |<span data-ttu-id="ff011-300">String</span><span class="sxs-lookup"><span data-stu-id="ff011-300">String</span></span> |
| <span data-ttu-id="ff011-301">year</span><span class="sxs-lookup"><span data-stu-id="ff011-301">year</span></span> |<span data-ttu-id="ff011-302">Int</span><span class="sxs-lookup"><span data-stu-id="ff011-302">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="ff011-303">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="ff011-303">Map source to sink columns</span></span>
<span data-ttu-id="ff011-304">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ff011-304">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="ff011-305">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="ff011-305">Repeatable read from relational sources</span></span>
<span data-ttu-id="ff011-306">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="ff011-306">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="ff011-307">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="ff011-307">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ff011-308">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="ff011-308">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ff011-309">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="ff011-309">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ff011-310">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ff011-310">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ff011-311">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="ff011-311">Performance and Tuning</span></span>
<span data-ttu-id="ff011-312">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="ff011-312">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
