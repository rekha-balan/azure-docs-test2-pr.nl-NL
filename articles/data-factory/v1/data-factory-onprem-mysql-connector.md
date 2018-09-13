---
title: Move data from MySQL using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from MySQL database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/06/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 34de57188dffb7375889ed9ed89a759238b035ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855870"
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="80589-103">Move data From MySQL using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="80589-103">Move data From MySQL using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-onprem-mysql-connector.md)
> * [Version 2 (current version)](../connector-mysql.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [MySQL connector in V2](../connector-mysql.md).


<span data-ttu-id="80589-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span><span class="sxs-lookup"><span data-stu-id="80589-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="80589-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="80589-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="80589-110">You can copy data from an on-premises MySQL data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="80589-110">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="80589-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="80589-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="80589-112">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span><span class="sxs-lookup"><span data-stu-id="80589-112">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="80589-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="80589-113">Prerequisites</span></span>
<span data-ttu-id="80589-114">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="80589-114">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="80589-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="80589-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="80589-116">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="80589-116">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="80589-117">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="80589-117">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.

## <a name="supported-versions-and-installation"></a><span data-ttu-id="80589-119">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="80589-119">Supported versions and installation</span></span>
<span data-ttu-id="80589-120">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version between 6.6.5 and 6.10.7) on the same system as the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="80589-120">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version between 6.6.5 and 6.10.7) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="80589-121">This 32 bit driver is compatible with 64 bit Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="80589-121">This 32 bit driver is compatible with 64 bit Data Management Gateway.</span></span> <span data-ttu-id="80589-122">MySQL version 5.1 and above is supported.</span><span class="sxs-lookup"><span data-stu-id="80589-122">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.

## <a name="getting-started"></a><span data-ttu-id="80589-124">Getting started</span><span class="sxs-lookup"><span data-stu-id="80589-124">Getting started</span></span>
<span data-ttu-id="80589-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="80589-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="80589-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="80589-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="80589-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="80589-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="80589-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="80589-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="80589-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="80589-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="80589-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="80589-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="80589-131">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="80589-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="80589-132">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="80589-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="80589-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="80589-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="80589-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="80589-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="80589-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="80589-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="80589-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="80589-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="80589-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span><span class="sxs-lookup"><span data-stu-id="80589-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="80589-138">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="80589-138">Linked service properties</span></span>
<span data-ttu-id="80589-139">The following table provides description for JSON elements specific to MySQL linked service.</span><span class="sxs-lookup"><span data-stu-id="80589-139">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="80589-140">Property</span><span class="sxs-lookup"><span data-stu-id="80589-140">Property</span></span> | <span data-ttu-id="80589-141">Description</span><span class="sxs-lookup"><span data-stu-id="80589-141">Description</span></span> | <span data-ttu-id="80589-142">Required</span><span class="sxs-lookup"><span data-stu-id="80589-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80589-143">type</span><span class="sxs-lookup"><span data-stu-id="80589-143">type</span></span> |<span data-ttu-id="80589-144">The type property must be set to: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="80589-144">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="80589-145">Yes</span><span class="sxs-lookup"><span data-stu-id="80589-145">Yes</span></span> |
| <span data-ttu-id="80589-146">server</span><span class="sxs-lookup"><span data-stu-id="80589-146">server</span></span> |<span data-ttu-id="80589-147">Name of the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="80589-147">Name of the MySQL server.</span></span> |<span data-ttu-id="80589-148">Yes</span><span class="sxs-lookup"><span data-stu-id="80589-148">Yes</span></span> |
| <span data-ttu-id="80589-149">database</span><span class="sxs-lookup"><span data-stu-id="80589-149">database</span></span> |<span data-ttu-id="80589-150">Name of the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="80589-150">Name of the MySQL database.</span></span> |<span data-ttu-id="80589-151">Yes</span><span class="sxs-lookup"><span data-stu-id="80589-151">Yes</span></span> |
| <span data-ttu-id="80589-152">schema</span><span class="sxs-lookup"><span data-stu-id="80589-152">schema</span></span> |<span data-ttu-id="80589-153">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="80589-153">Name of the schema in the database.</span></span> |<span data-ttu-id="80589-154">No</span><span class="sxs-lookup"><span data-stu-id="80589-154">No</span></span> |
| <span data-ttu-id="80589-155">authenticationType</span><span class="sxs-lookup"><span data-stu-id="80589-155">authenticationType</span></span> |<span data-ttu-id="80589-156">Type of authentication used to connect to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="80589-156">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="80589-157">Possible values are: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="80589-157">Possible values are: `Basic`.</span></span> |<span data-ttu-id="80589-158">Yes</span><span class="sxs-lookup"><span data-stu-id="80589-158">Yes</span></span> |
| <span data-ttu-id="80589-159">username</span><span class="sxs-lookup"><span data-stu-id="80589-159">username</span></span> |<span data-ttu-id="80589-160">Specify user name to connect to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="80589-160">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="80589-161">Yes</span><span class="sxs-lookup"><span data-stu-id="80589-161">Yes</span></span> |
| <span data-ttu-id="80589-162">password</span><span class="sxs-lookup"><span data-stu-id="80589-162">password</span></span> |<span data-ttu-id="80589-163">Specify password for the user account you specified.</span><span class="sxs-lookup"><span data-stu-id="80589-163">Specify password for the user account you specified.</span></span> |<span data-ttu-id="80589-164">Yes</span><span class="sxs-lookup"><span data-stu-id="80589-164">Yes</span></span> |
| <span data-ttu-id="80589-165">gatewayName</span><span class="sxs-lookup"><span data-stu-id="80589-165">gatewayName</span></span> |<span data-ttu-id="80589-166">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span><span class="sxs-lookup"><span data-stu-id="80589-166">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="80589-167">Yes</span><span class="sxs-lookup"><span data-stu-id="80589-167">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="80589-168">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="80589-168">Dataset properties</span></span>
<span data-ttu-id="80589-169">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="80589-169">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="80589-170">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="80589-170">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="80589-171">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="80589-171">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="80589-172">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span><span class="sxs-lookup"><span data-stu-id="80589-172">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="80589-173">Property</span><span class="sxs-lookup"><span data-stu-id="80589-173">Property</span></span> | <span data-ttu-id="80589-174">Description</span><span class="sxs-lookup"><span data-stu-id="80589-174">Description</span></span> | <span data-ttu-id="80589-175">Required</span><span class="sxs-lookup"><span data-stu-id="80589-175">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80589-176">tableName</span><span class="sxs-lookup"><span data-stu-id="80589-176">tableName</span></span> |<span data-ttu-id="80589-177">Name of the table in the MySQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="80589-177">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="80589-178">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="80589-178">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="80589-179">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="80589-179">Copy activity properties</span></span>
<span data-ttu-id="80589-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="80589-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="80589-181">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="80589-181">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="80589-182">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="80589-182">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="80589-183">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="80589-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="80589-184">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="80589-184">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="80589-185">Property</span><span class="sxs-lookup"><span data-stu-id="80589-185">Property</span></span> | <span data-ttu-id="80589-186">Description</span><span class="sxs-lookup"><span data-stu-id="80589-186">Description</span></span> | <span data-ttu-id="80589-187">Allowed values</span><span class="sxs-lookup"><span data-stu-id="80589-187">Allowed values</span></span> | <span data-ttu-id="80589-188">Required</span><span class="sxs-lookup"><span data-stu-id="80589-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="80589-189">query</span><span class="sxs-lookup"><span data-stu-id="80589-189">query</span></span> |<span data-ttu-id="80589-190">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="80589-190">Use the custom query to read data.</span></span> |<span data-ttu-id="80589-191">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="80589-191">SQL query string.</span></span> <span data-ttu-id="80589-192">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="80589-192">For example: select \* from MyTable.</span></span> |<span data-ttu-id="80589-193">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="80589-193">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="80589-194">JSON example: Copy data from MySQL to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="80589-194">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="80589-195">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="80589-195">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="80589-196">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="80589-196">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="80589-197">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="80589-197">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> This sample provides JSON snippets. It does not include step-by-step instructions for creating the data factory. See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.

<span data-ttu-id="80589-201">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="80589-201">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="80589-202">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="80589-202">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="80589-203">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="80589-203">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="80589-204">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="80589-204">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="80589-205">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="80589-205">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="80589-206">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="80589-206">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="80589-207">The sample copies data from a query result in MySQL database to a blob hourly.</span><span class="sxs-lookup"><span data-stu-id="80589-207">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="80589-208">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="80589-208">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="80589-209">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="80589-209">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="80589-210">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="80589-210">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="80589-211">**MySQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="80589-211">**MySQL linked service:**</span></span>

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

<span data-ttu-id="80589-212">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="80589-212">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="80589-213">**MySQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="80589-213">**MySQL input dataset:**</span></span>

<span data-ttu-id="80589-214">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="80589-214">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="80589-215">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="80589-215">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="80589-216">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="80589-216">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="80589-217">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="80589-217">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="80589-218">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="80589-218">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="80589-219">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="80589-219">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="80589-220">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="80589-220">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="80589-221">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="80589-221">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="80589-222">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="80589-222">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="80589-223">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="80589-223">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="80589-224">Type mapping for MySQL</span><span class="sxs-lookup"><span data-stu-id="80589-224">Type mapping for MySQL</span></span>
<span data-ttu-id="80589-225">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span><span class="sxs-lookup"><span data-stu-id="80589-225">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="80589-226">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="80589-226">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="80589-227">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="80589-227">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="80589-228">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span><span class="sxs-lookup"><span data-stu-id="80589-228">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="80589-229">MySQL Database type</span><span class="sxs-lookup"><span data-stu-id="80589-229">MySQL Database type</span></span> | <span data-ttu-id="80589-230">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="80589-230">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="80589-231">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="80589-231">bigint unsigned</span></span> |<span data-ttu-id="80589-232">Decimal</span><span class="sxs-lookup"><span data-stu-id="80589-232">Decimal</span></span> |
| <span data-ttu-id="80589-233">bigint</span><span class="sxs-lookup"><span data-stu-id="80589-233">bigint</span></span> |<span data-ttu-id="80589-234">Int64</span><span class="sxs-lookup"><span data-stu-id="80589-234">Int64</span></span> |
| <span data-ttu-id="80589-235">bit</span><span class="sxs-lookup"><span data-stu-id="80589-235">bit</span></span> |<span data-ttu-id="80589-236">Decimal</span><span class="sxs-lookup"><span data-stu-id="80589-236">Decimal</span></span> |
| <span data-ttu-id="80589-237">blob</span><span class="sxs-lookup"><span data-stu-id="80589-237">blob</span></span> |<span data-ttu-id="80589-238">Byte[]</span><span class="sxs-lookup"><span data-stu-id="80589-238">Byte[]</span></span> |
| <span data-ttu-id="80589-239">bool</span><span class="sxs-lookup"><span data-stu-id="80589-239">bool</span></span> |<span data-ttu-id="80589-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="80589-240">Boolean</span></span> |
| <span data-ttu-id="80589-241">char</span><span class="sxs-lookup"><span data-stu-id="80589-241">char</span></span> |<span data-ttu-id="80589-242">String</span><span class="sxs-lookup"><span data-stu-id="80589-242">String</span></span> |
| <span data-ttu-id="80589-243">date</span><span class="sxs-lookup"><span data-stu-id="80589-243">date</span></span> |<span data-ttu-id="80589-244">Datetime</span><span class="sxs-lookup"><span data-stu-id="80589-244">Datetime</span></span> |
| <span data-ttu-id="80589-245">datetime</span><span class="sxs-lookup"><span data-stu-id="80589-245">datetime</span></span> |<span data-ttu-id="80589-246">Datetime</span><span class="sxs-lookup"><span data-stu-id="80589-246">Datetime</span></span> |
| <span data-ttu-id="80589-247">decimal</span><span class="sxs-lookup"><span data-stu-id="80589-247">decimal</span></span> |<span data-ttu-id="80589-248">Decimal</span><span class="sxs-lookup"><span data-stu-id="80589-248">Decimal</span></span> |
| <span data-ttu-id="80589-249">double precision</span><span class="sxs-lookup"><span data-stu-id="80589-249">double precision</span></span> |<span data-ttu-id="80589-250">Double</span><span class="sxs-lookup"><span data-stu-id="80589-250">Double</span></span> |
| <span data-ttu-id="80589-251">double</span><span class="sxs-lookup"><span data-stu-id="80589-251">double</span></span> |<span data-ttu-id="80589-252">Double</span><span class="sxs-lookup"><span data-stu-id="80589-252">Double</span></span> |
| <span data-ttu-id="80589-253">enum</span><span class="sxs-lookup"><span data-stu-id="80589-253">enum</span></span> |<span data-ttu-id="80589-254">String</span><span class="sxs-lookup"><span data-stu-id="80589-254">String</span></span> |
| <span data-ttu-id="80589-255">float</span><span class="sxs-lookup"><span data-stu-id="80589-255">float</span></span> |<span data-ttu-id="80589-256">Single</span><span class="sxs-lookup"><span data-stu-id="80589-256">Single</span></span> |
| <span data-ttu-id="80589-257">int unsigned</span><span class="sxs-lookup"><span data-stu-id="80589-257">int unsigned</span></span> |<span data-ttu-id="80589-258">Int64</span><span class="sxs-lookup"><span data-stu-id="80589-258">Int64</span></span> |
| <span data-ttu-id="80589-259">int</span><span class="sxs-lookup"><span data-stu-id="80589-259">int</span></span> |<span data-ttu-id="80589-260">Int32</span><span class="sxs-lookup"><span data-stu-id="80589-260">Int32</span></span> |
| <span data-ttu-id="80589-261">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="80589-261">integer unsigned</span></span> |<span data-ttu-id="80589-262">Int64</span><span class="sxs-lookup"><span data-stu-id="80589-262">Int64</span></span> |
| <span data-ttu-id="80589-263">integer</span><span class="sxs-lookup"><span data-stu-id="80589-263">integer</span></span> |<span data-ttu-id="80589-264">Int32</span><span class="sxs-lookup"><span data-stu-id="80589-264">Int32</span></span> |
| <span data-ttu-id="80589-265">long varbinary</span><span class="sxs-lookup"><span data-stu-id="80589-265">long varbinary</span></span> |<span data-ttu-id="80589-266">Byte[]</span><span class="sxs-lookup"><span data-stu-id="80589-266">Byte[]</span></span> |
| <span data-ttu-id="80589-267">long varchar</span><span class="sxs-lookup"><span data-stu-id="80589-267">long varchar</span></span> |<span data-ttu-id="80589-268">String</span><span class="sxs-lookup"><span data-stu-id="80589-268">String</span></span> |
| <span data-ttu-id="80589-269">longblob</span><span class="sxs-lookup"><span data-stu-id="80589-269">longblob</span></span> |<span data-ttu-id="80589-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="80589-270">Byte[]</span></span> |
| <span data-ttu-id="80589-271">longtext</span><span class="sxs-lookup"><span data-stu-id="80589-271">longtext</span></span> |<span data-ttu-id="80589-272">String</span><span class="sxs-lookup"><span data-stu-id="80589-272">String</span></span> |
| <span data-ttu-id="80589-273">mediumblob</span><span class="sxs-lookup"><span data-stu-id="80589-273">mediumblob</span></span> |<span data-ttu-id="80589-274">Byte[]</span><span class="sxs-lookup"><span data-stu-id="80589-274">Byte[]</span></span> |
| <span data-ttu-id="80589-275">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="80589-275">mediumint unsigned</span></span> |<span data-ttu-id="80589-276">Int64</span><span class="sxs-lookup"><span data-stu-id="80589-276">Int64</span></span> |
| <span data-ttu-id="80589-277">mediumint</span><span class="sxs-lookup"><span data-stu-id="80589-277">mediumint</span></span> |<span data-ttu-id="80589-278">Int32</span><span class="sxs-lookup"><span data-stu-id="80589-278">Int32</span></span> |
| <span data-ttu-id="80589-279">mediumtext</span><span class="sxs-lookup"><span data-stu-id="80589-279">mediumtext</span></span> |<span data-ttu-id="80589-280">String</span><span class="sxs-lookup"><span data-stu-id="80589-280">String</span></span> |
| <span data-ttu-id="80589-281">numeric</span><span class="sxs-lookup"><span data-stu-id="80589-281">numeric</span></span> |<span data-ttu-id="80589-282">Decimal</span><span class="sxs-lookup"><span data-stu-id="80589-282">Decimal</span></span> |
| <span data-ttu-id="80589-283">real</span><span class="sxs-lookup"><span data-stu-id="80589-283">real</span></span> |<span data-ttu-id="80589-284">Double</span><span class="sxs-lookup"><span data-stu-id="80589-284">Double</span></span> |
| <span data-ttu-id="80589-285">set</span><span class="sxs-lookup"><span data-stu-id="80589-285">set</span></span> |<span data-ttu-id="80589-286">String</span><span class="sxs-lookup"><span data-stu-id="80589-286">String</span></span> |
| <span data-ttu-id="80589-287">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="80589-287">smallint unsigned</span></span> |<span data-ttu-id="80589-288">Int32</span><span class="sxs-lookup"><span data-stu-id="80589-288">Int32</span></span> |
| <span data-ttu-id="80589-289">smallint</span><span class="sxs-lookup"><span data-stu-id="80589-289">smallint</span></span> |<span data-ttu-id="80589-290">Int16</span><span class="sxs-lookup"><span data-stu-id="80589-290">Int16</span></span> |
| <span data-ttu-id="80589-291">text</span><span class="sxs-lookup"><span data-stu-id="80589-291">text</span></span> |<span data-ttu-id="80589-292">String</span><span class="sxs-lookup"><span data-stu-id="80589-292">String</span></span> |
| <span data-ttu-id="80589-293">time</span><span class="sxs-lookup"><span data-stu-id="80589-293">time</span></span> |<span data-ttu-id="80589-294">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="80589-294">TimeSpan</span></span> |
| <span data-ttu-id="80589-295">timestamp</span><span class="sxs-lookup"><span data-stu-id="80589-295">timestamp</span></span> |<span data-ttu-id="80589-296">Datetime</span><span class="sxs-lookup"><span data-stu-id="80589-296">Datetime</span></span> |
| <span data-ttu-id="80589-297">tinyblob</span><span class="sxs-lookup"><span data-stu-id="80589-297">tinyblob</span></span> |<span data-ttu-id="80589-298">Byte[]</span><span class="sxs-lookup"><span data-stu-id="80589-298">Byte[]</span></span> |
| <span data-ttu-id="80589-299">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="80589-299">tinyint unsigned</span></span> |<span data-ttu-id="80589-300">Int16</span><span class="sxs-lookup"><span data-stu-id="80589-300">Int16</span></span> |
| <span data-ttu-id="80589-301">tinyint</span><span class="sxs-lookup"><span data-stu-id="80589-301">tinyint</span></span> |<span data-ttu-id="80589-302">Int16</span><span class="sxs-lookup"><span data-stu-id="80589-302">Int16</span></span> |
| <span data-ttu-id="80589-303">tinytext</span><span class="sxs-lookup"><span data-stu-id="80589-303">tinytext</span></span> |<span data-ttu-id="80589-304">String</span><span class="sxs-lookup"><span data-stu-id="80589-304">String</span></span> |
| <span data-ttu-id="80589-305">varchar</span><span class="sxs-lookup"><span data-stu-id="80589-305">varchar</span></span> |<span data-ttu-id="80589-306">String</span><span class="sxs-lookup"><span data-stu-id="80589-306">String</span></span> |
| <span data-ttu-id="80589-307">year</span><span class="sxs-lookup"><span data-stu-id="80589-307">year</span></span> |<span data-ttu-id="80589-308">Int</span><span class="sxs-lookup"><span data-stu-id="80589-308">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="80589-309">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="80589-309">Map source to sink columns</span></span>
<span data-ttu-id="80589-310">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="80589-310">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="80589-311">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="80589-311">Repeatable read from relational sources</span></span>
<span data-ttu-id="80589-312">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="80589-312">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="80589-313">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="80589-313">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="80589-314">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="80589-314">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="80589-315">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="80589-315">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="80589-316">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="80589-316">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="80589-317">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="80589-317">Performance and Tuning</span></span>
<span data-ttu-id="80589-318">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="80589-318">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
