---
title: Move data From PostgreSQL using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from PostgreSQL Database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2017
ms.author: jingwang
ms.openlocfilehash: bd6892c4b50612dc3fd27b1c7e4626c6257c0c9e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553319"
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="3420e-103">Move data from PostgreSQL using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3420e-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="3420e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="3420e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="3420e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="3420e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="3420e-106">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="3420e-106">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span></span> <span data-ttu-id="3420e-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="3420e-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3420e-108">Data factory currently supports only moving data from a PostgreSQL data store to other data stores, but not for moving data from other data stores to an PostgreSQL data store.</span><span class="sxs-lookup"><span data-stu-id="3420e-108">Data factory currently supports only moving data from a PostgreSQL data store to other data stores, but not for moving data from other data stores to an PostgreSQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3420e-109">prerequisites</span><span class="sxs-lookup"><span data-stu-id="3420e-109">prerequisites</span></span>

<span data-ttu-id="3420e-110">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="3420e-110">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="3420e-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="3420e-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="3420e-112">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="3420e-112">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="3420e-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="3420e-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="3420e-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="3420e-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="3420e-115">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="3420e-115">Supported versions and installation</span></span>
<span data-ttu-id="3420e-116">For Data Management Gateway to connect to the PostgreSQL Database, you need to install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on the same system as the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="3420e-116">For Data Management Gateway to connect to the PostgreSQL Database, you need to install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="3420e-117">PostgreSQL version 7.4 and above is supported.</span><span class="sxs-lookup"><span data-stu-id="3420e-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3420e-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="3420e-118">Getting started</span></span>
<span data-ttu-id="3420e-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="3420e-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="3420e-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="3420e-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="3420e-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="3420e-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="3420e-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="3420e-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3420e-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="3420e-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3420e-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="3420e-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="3420e-125">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="3420e-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="3420e-126">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="3420e-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="3420e-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="3420e-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3420e-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="3420e-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="3420e-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="3420e-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="3420e-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="3420e-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3420e-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span><span class="sxs-lookup"><span data-stu-id="3420e-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3420e-132">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="3420e-132">Linked service properties</span></span>
<span data-ttu-id="3420e-133">The following table provides description for JSON elements specific to PostgreSQL linked service.</span><span class="sxs-lookup"><span data-stu-id="3420e-133">The following table provides description for JSON elements specific to PostgreSQL linked service.</span></span>

| <span data-ttu-id="3420e-134">Property</span><span class="sxs-lookup"><span data-stu-id="3420e-134">Property</span></span> | <span data-ttu-id="3420e-135">Description</span><span class="sxs-lookup"><span data-stu-id="3420e-135">Description</span></span> | <span data-ttu-id="3420e-136">Required</span><span class="sxs-lookup"><span data-stu-id="3420e-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3420e-137">type</span><span class="sxs-lookup"><span data-stu-id="3420e-137">type</span></span> |<span data-ttu-id="3420e-138">The type property must be set to: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="3420e-138">The type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="3420e-139">Yes</span><span class="sxs-lookup"><span data-stu-id="3420e-139">Yes</span></span> |
| <span data-ttu-id="3420e-140">server</span><span class="sxs-lookup"><span data-stu-id="3420e-140">server</span></span> |<span data-ttu-id="3420e-141">Name of the PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="3420e-141">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="3420e-142">Yes</span><span class="sxs-lookup"><span data-stu-id="3420e-142">Yes</span></span> |
| <span data-ttu-id="3420e-143">database</span><span class="sxs-lookup"><span data-stu-id="3420e-143">database</span></span> |<span data-ttu-id="3420e-144">Name of the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="3420e-144">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="3420e-145">Yes</span><span class="sxs-lookup"><span data-stu-id="3420e-145">Yes</span></span> |
| <span data-ttu-id="3420e-146">schema</span><span class="sxs-lookup"><span data-stu-id="3420e-146">schema</span></span> |<span data-ttu-id="3420e-147">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="3420e-147">Name of the schema in the database.</span></span> <span data-ttu-id="3420e-148">The schema name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="3420e-148">The schema name is case-sensitive.</span></span> |<span data-ttu-id="3420e-149">No</span><span class="sxs-lookup"><span data-stu-id="3420e-149">No</span></span> |
| <span data-ttu-id="3420e-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3420e-150">authenticationType</span></span> |<span data-ttu-id="3420e-151">Type of authentication used to connect to the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="3420e-151">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="3420e-152">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="3420e-152">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="3420e-153">Yes</span><span class="sxs-lookup"><span data-stu-id="3420e-153">Yes</span></span> |
| <span data-ttu-id="3420e-154">username</span><span class="sxs-lookup"><span data-stu-id="3420e-154">username</span></span> |<span data-ttu-id="3420e-155">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="3420e-155">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="3420e-156">No</span><span class="sxs-lookup"><span data-stu-id="3420e-156">No</span></span> |
| <span data-ttu-id="3420e-157">password</span><span class="sxs-lookup"><span data-stu-id="3420e-157">password</span></span> |<span data-ttu-id="3420e-158">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="3420e-158">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3420e-159">No</span><span class="sxs-lookup"><span data-stu-id="3420e-159">No</span></span> |
| <span data-ttu-id="3420e-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3420e-160">gatewayName</span></span> |<span data-ttu-id="3420e-161">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="3420e-161">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="3420e-162">Yes</span><span class="sxs-lookup"><span data-stu-id="3420e-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="3420e-163">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="3420e-163">Dataset properties</span></span>
<span data-ttu-id="3420e-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="3420e-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3420e-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="3420e-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3420e-166">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="3420e-166">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="3420e-167">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span><span class="sxs-lookup"><span data-stu-id="3420e-167">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span></span>

| <span data-ttu-id="3420e-168">Property</span><span class="sxs-lookup"><span data-stu-id="3420e-168">Property</span></span> | <span data-ttu-id="3420e-169">Description</span><span class="sxs-lookup"><span data-stu-id="3420e-169">Description</span></span> | <span data-ttu-id="3420e-170">Required</span><span class="sxs-lookup"><span data-stu-id="3420e-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3420e-171">tableName</span><span class="sxs-lookup"><span data-stu-id="3420e-171">tableName</span></span> |<span data-ttu-id="3420e-172">Name of the table in the PostgreSQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="3420e-172">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="3420e-173">The tableName is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="3420e-173">The tableName is case-sensitive.</span></span> |<span data-ttu-id="3420e-174">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="3420e-174">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="3420e-175">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="3420e-175">Copy activity properties</span></span>
<span data-ttu-id="3420e-176">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="3420e-176">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3420e-177">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="3420e-177">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="3420e-178">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="3420e-178">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="3420e-179">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="3420e-179">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="3420e-180">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="3420e-180">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="3420e-181">Property</span><span class="sxs-lookup"><span data-stu-id="3420e-181">Property</span></span> | <span data-ttu-id="3420e-182">Description</span><span class="sxs-lookup"><span data-stu-id="3420e-182">Description</span></span> | <span data-ttu-id="3420e-183">Allowed values</span><span class="sxs-lookup"><span data-stu-id="3420e-183">Allowed values</span></span> | <span data-ttu-id="3420e-184">Required</span><span class="sxs-lookup"><span data-stu-id="3420e-184">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3420e-185">query</span><span class="sxs-lookup"><span data-stu-id="3420e-185">query</span></span> |<span data-ttu-id="3420e-186">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="3420e-186">Use the custom query to read data.</span></span> |<span data-ttu-id="3420e-187">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="3420e-187">SQL query string.</span></span> <span data-ttu-id="3420e-188">For example: "query": "select \* from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="3420e-188">For example: "query": "select \* from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="3420e-189">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="3420e-189">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="3420e-190">Schema and table names are case-sensitive and they have to  be enclosed in `""` (double quotes) in the query.</span><span class="sxs-lookup"><span data-stu-id="3420e-190">Schema and table names are case-sensitive and they have to  be enclosed in `""` (double quotes) in the query.</span></span>  

<span data-ttu-id="3420e-191">**Example:**</span><span class="sxs-lookup"><span data-stu-id="3420e-191">**Example:**</span></span>

 <span data-ttu-id="3420e-192">"query": "select \* from \"MySchema\".\"MyTable\""</span><span class="sxs-lookup"><span data-stu-id="3420e-192">"query": "select \* from \"MySchema\".\"MyTable\""</span></span>

## <a name="json-example-copy-data-from-postgresql-to-azure-blob"></a><span data-ttu-id="3420e-193">JSON example: Copy data from PostgreSQL to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="3420e-193">JSON example: Copy data from PostgreSQL to Azure Blob</span></span>
<span data-ttu-id="3420e-194">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3420e-194">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3420e-195">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3420e-195">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span></span> <span data-ttu-id="3420e-196">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3420e-196">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="3420e-197">This sample provides JSON snippets.</span><span class="sxs-lookup"><span data-stu-id="3420e-197">This sample provides JSON snippets.</span></span> <span data-ttu-id="3420e-198">It does not include step-by-step instructions for creating the data factory.</span><span class="sxs-lookup"><span data-stu-id="3420e-198">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="3420e-199">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="3420e-199">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="3420e-200">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="3420e-200">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="3420e-201">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3420e-201">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="3420e-202">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3420e-202">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3420e-203">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3420e-203">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="3420e-204">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3420e-204">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3420e-205">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3420e-205">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3420e-206">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="3420e-206">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span></span> <span data-ttu-id="3420e-207">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="3420e-207">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="3420e-208">As a first step, setup the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="3420e-208">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="3420e-209">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="3420e-209">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="3420e-210">**PostgreSQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="3420e-210">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
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
<span data-ttu-id="3420e-211">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="3420e-211">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="3420e-212">**PostgreSQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="3420e-212">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="3420e-213">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span><span class="sxs-lookup"><span data-stu-id="3420e-213">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="3420e-214">Setting “external”: true informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="3420e-214">Setting “external”: true informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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

<span data-ttu-id="3420e-215">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="3420e-215">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="3420e-216">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="3420e-216">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3420e-217">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="3420e-217">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3420e-218">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="3420e-218">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="3420e-219">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="3420e-219">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="3420e-220">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span><span class="sxs-lookup"><span data-stu-id="3420e-220">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="3420e-221">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3420e-221">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="3420e-222">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="3420e-222">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="3420e-223">Type mapping for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3420e-223">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="3420e-224">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="3420e-224">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="3420e-225">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="3420e-225">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="3420e-226">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="3420e-226">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="3420e-227">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span><span class="sxs-lookup"><span data-stu-id="3420e-227">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span></span>

| <span data-ttu-id="3420e-228">PostgreSQL Database type</span><span class="sxs-lookup"><span data-stu-id="3420e-228">PostgreSQL Database type</span></span> | <span data-ttu-id="3420e-229">PostgresSQL aliases</span><span class="sxs-lookup"><span data-stu-id="3420e-229">PostgresSQL aliases</span></span> | <span data-ttu-id="3420e-230">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="3420e-230">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3420e-231">abstime</span><span class="sxs-lookup"><span data-stu-id="3420e-231">abstime</span></span> | |<span data-ttu-id="3420e-232">Datetime</span><span class="sxs-lookup"><span data-stu-id="3420e-232">Datetime</span></span> | &nbsp;
| <span data-ttu-id="3420e-233">bigint</span><span class="sxs-lookup"><span data-stu-id="3420e-233">bigint</span></span> |<span data-ttu-id="3420e-234">int8</span><span class="sxs-lookup"><span data-stu-id="3420e-234">int8</span></span> |<span data-ttu-id="3420e-235">Int64</span><span class="sxs-lookup"><span data-stu-id="3420e-235">Int64</span></span> |
| <span data-ttu-id="3420e-236">bigserial</span><span class="sxs-lookup"><span data-stu-id="3420e-236">bigserial</span></span> |<span data-ttu-id="3420e-237">serial8</span><span class="sxs-lookup"><span data-stu-id="3420e-237">serial8</span></span> |<span data-ttu-id="3420e-238">Int64</span><span class="sxs-lookup"><span data-stu-id="3420e-238">Int64</span></span> |
| <span data-ttu-id="3420e-239">bit [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-239">bit [ (n) ]</span></span> | |<span data-ttu-id="3420e-240">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-240">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="3420e-241">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-241">bit varying [ (n) ]</span></span> |<span data-ttu-id="3420e-242">varbit</span><span class="sxs-lookup"><span data-stu-id="3420e-242">varbit</span></span> |<span data-ttu-id="3420e-243">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-243">Byte[], String</span></span> |
| <span data-ttu-id="3420e-244">boolean</span><span class="sxs-lookup"><span data-stu-id="3420e-244">boolean</span></span> |<span data-ttu-id="3420e-245">bool</span><span class="sxs-lookup"><span data-stu-id="3420e-245">bool</span></span> |<span data-ttu-id="3420e-246">Boolean</span><span class="sxs-lookup"><span data-stu-id="3420e-246">Boolean</span></span> |
| <span data-ttu-id="3420e-247">box</span><span class="sxs-lookup"><span data-stu-id="3420e-247">box</span></span> | |<span data-ttu-id="3420e-248">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-248">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-249">bytea</span><span class="sxs-lookup"><span data-stu-id="3420e-249">bytea</span></span> | |<span data-ttu-id="3420e-250">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-250">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-251">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-251">character [ (n) ]</span></span> |<span data-ttu-id="3420e-252">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-252">char [ (n) ]</span></span> |<span data-ttu-id="3420e-253">String</span><span class="sxs-lookup"><span data-stu-id="3420e-253">String</span></span> |
| <span data-ttu-id="3420e-254">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-254">character varying [ (n) ]</span></span> |<span data-ttu-id="3420e-255">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-255">varchar [ (n) ]</span></span> |<span data-ttu-id="3420e-256">String</span><span class="sxs-lookup"><span data-stu-id="3420e-256">String</span></span> |
| <span data-ttu-id="3420e-257">cid</span><span class="sxs-lookup"><span data-stu-id="3420e-257">cid</span></span> | |<span data-ttu-id="3420e-258">String</span><span class="sxs-lookup"><span data-stu-id="3420e-258">String</span></span> |&nbsp;
| <span data-ttu-id="3420e-259">cidr</span><span class="sxs-lookup"><span data-stu-id="3420e-259">cidr</span></span> | |<span data-ttu-id="3420e-260">String</span><span class="sxs-lookup"><span data-stu-id="3420e-260">String</span></span> |&nbsp;
| <span data-ttu-id="3420e-261">circle</span><span class="sxs-lookup"><span data-stu-id="3420e-261">circle</span></span> | |<span data-ttu-id="3420e-262">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-262">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-263">date</span><span class="sxs-lookup"><span data-stu-id="3420e-263">date</span></span> | |<span data-ttu-id="3420e-264">Datetime</span><span class="sxs-lookup"><span data-stu-id="3420e-264">Datetime</span></span> |&nbsp;
| <span data-ttu-id="3420e-265">daterange</span><span class="sxs-lookup"><span data-stu-id="3420e-265">daterange</span></span> | |<span data-ttu-id="3420e-266">String</span><span class="sxs-lookup"><span data-stu-id="3420e-266">String</span></span> |&nbsp;
| <span data-ttu-id="3420e-267">double precision</span><span class="sxs-lookup"><span data-stu-id="3420e-267">double precision</span></span> |<span data-ttu-id="3420e-268">float8</span><span class="sxs-lookup"><span data-stu-id="3420e-268">float8</span></span> |<span data-ttu-id="3420e-269">Double</span><span class="sxs-lookup"><span data-stu-id="3420e-269">Double</span></span> |
| <span data-ttu-id="3420e-270">inet</span><span class="sxs-lookup"><span data-stu-id="3420e-270">inet</span></span> | |<span data-ttu-id="3420e-271">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-271">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-272">intarry</span><span class="sxs-lookup"><span data-stu-id="3420e-272">intarry</span></span> | |<span data-ttu-id="3420e-273">String</span><span class="sxs-lookup"><span data-stu-id="3420e-273">String</span></span> |&nbsp;
| <span data-ttu-id="3420e-274">int4range</span><span class="sxs-lookup"><span data-stu-id="3420e-274">int4range</span></span> | |<span data-ttu-id="3420e-275">String</span><span class="sxs-lookup"><span data-stu-id="3420e-275">String</span></span> |&nbsp;
| <span data-ttu-id="3420e-276">int8range</span><span class="sxs-lookup"><span data-stu-id="3420e-276">int8range</span></span> | |<span data-ttu-id="3420e-277">String</span><span class="sxs-lookup"><span data-stu-id="3420e-277">String</span></span> |&nbsp;
| <span data-ttu-id="3420e-278">integer</span><span class="sxs-lookup"><span data-stu-id="3420e-278">integer</span></span> |<span data-ttu-id="3420e-279">int, int4</span><span class="sxs-lookup"><span data-stu-id="3420e-279">int, int4</span></span> |<span data-ttu-id="3420e-280">Int32</span><span class="sxs-lookup"><span data-stu-id="3420e-280">Int32</span></span> |
| <span data-ttu-id="3420e-281">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-281">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="3420e-282">Timespan</span><span class="sxs-lookup"><span data-stu-id="3420e-282">Timespan</span></span> |&nbsp;
| <span data-ttu-id="3420e-283">json</span><span class="sxs-lookup"><span data-stu-id="3420e-283">json</span></span> | |<span data-ttu-id="3420e-284">String</span><span class="sxs-lookup"><span data-stu-id="3420e-284">String</span></span> |&nbsp;
| <span data-ttu-id="3420e-285">jsonb</span><span class="sxs-lookup"><span data-stu-id="3420e-285">jsonb</span></span> | |<span data-ttu-id="3420e-286">Byte[]</span><span class="sxs-lookup"><span data-stu-id="3420e-286">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="3420e-287">line</span><span class="sxs-lookup"><span data-stu-id="3420e-287">line</span></span> | |<span data-ttu-id="3420e-288">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-288">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-289">lseg</span><span class="sxs-lookup"><span data-stu-id="3420e-289">lseg</span></span> | |<span data-ttu-id="3420e-290">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-290">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-291">macaddr</span><span class="sxs-lookup"><span data-stu-id="3420e-291">macaddr</span></span> | |<span data-ttu-id="3420e-292">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-292">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-293">money</span><span class="sxs-lookup"><span data-stu-id="3420e-293">money</span></span> | |<span data-ttu-id="3420e-294">Decimal</span><span class="sxs-lookup"><span data-stu-id="3420e-294">Decimal</span></span> |&nbsp;
| <span data-ttu-id="3420e-295">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-295">numeric [ (p, s) ]</span></span> |<span data-ttu-id="3420e-296">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="3420e-296">decimal [ (p, s) ]</span></span> |<span data-ttu-id="3420e-297">Decimal</span><span class="sxs-lookup"><span data-stu-id="3420e-297">Decimal</span></span> |
| <span data-ttu-id="3420e-298">numrange</span><span class="sxs-lookup"><span data-stu-id="3420e-298">numrange</span></span> | |<span data-ttu-id="3420e-299">String</span><span class="sxs-lookup"><span data-stu-id="3420e-299">String</span></span> |&nbsp;
| <span data-ttu-id="3420e-300">oid</span><span class="sxs-lookup"><span data-stu-id="3420e-300">oid</span></span> | |<span data-ttu-id="3420e-301">Int32</span><span class="sxs-lookup"><span data-stu-id="3420e-301">Int32</span></span> |&nbsp;
| <span data-ttu-id="3420e-302">path</span><span class="sxs-lookup"><span data-stu-id="3420e-302">path</span></span> | |<span data-ttu-id="3420e-303">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-303">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-304">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="3420e-304">pg_lsn</span></span> | |<span data-ttu-id="3420e-305">Int64</span><span class="sxs-lookup"><span data-stu-id="3420e-305">Int64</span></span> |&nbsp;
| <span data-ttu-id="3420e-306">point</span><span class="sxs-lookup"><span data-stu-id="3420e-306">point</span></span> | |<span data-ttu-id="3420e-307">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-307">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-308">polygon</span><span class="sxs-lookup"><span data-stu-id="3420e-308">polygon</span></span> | |<span data-ttu-id="3420e-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="3420e-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="3420e-310">real</span><span class="sxs-lookup"><span data-stu-id="3420e-310">real</span></span> |<span data-ttu-id="3420e-311">float4</span><span class="sxs-lookup"><span data-stu-id="3420e-311">float4</span></span> |<span data-ttu-id="3420e-312">Single</span><span class="sxs-lookup"><span data-stu-id="3420e-312">Single</span></span> |
| <span data-ttu-id="3420e-313">smallint</span><span class="sxs-lookup"><span data-stu-id="3420e-313">smallint</span></span> |<span data-ttu-id="3420e-314">int2</span><span class="sxs-lookup"><span data-stu-id="3420e-314">int2</span></span> |<span data-ttu-id="3420e-315">Int16</span><span class="sxs-lookup"><span data-stu-id="3420e-315">Int16</span></span> |
| <span data-ttu-id="3420e-316">smallserial</span><span class="sxs-lookup"><span data-stu-id="3420e-316">smallserial</span></span> |<span data-ttu-id="3420e-317">serial2</span><span class="sxs-lookup"><span data-stu-id="3420e-317">serial2</span></span> |<span data-ttu-id="3420e-318">Int16</span><span class="sxs-lookup"><span data-stu-id="3420e-318">Int16</span></span> |
| <span data-ttu-id="3420e-319">serial</span><span class="sxs-lookup"><span data-stu-id="3420e-319">serial</span></span> |<span data-ttu-id="3420e-320">serial4</span><span class="sxs-lookup"><span data-stu-id="3420e-320">serial4</span></span> |<span data-ttu-id="3420e-321">Int32</span><span class="sxs-lookup"><span data-stu-id="3420e-321">Int32</span></span> |
| <span data-ttu-id="3420e-322">text</span><span class="sxs-lookup"><span data-stu-id="3420e-322">text</span></span> | |<span data-ttu-id="3420e-323">String</span><span class="sxs-lookup"><span data-stu-id="3420e-323">String</span></span> |&nbsp;

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="3420e-324">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="3420e-324">Map source to sink columns</span></span>
<span data-ttu-id="3420e-325">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3420e-325">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3420e-326">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="3420e-326">Repeatable read from relational sources</span></span>
<span data-ttu-id="3420e-327">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="3420e-327">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="3420e-328">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="3420e-328">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3420e-329">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="3420e-329">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3420e-330">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="3420e-330">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3420e-331">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="3420e-331">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3420e-332">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="3420e-332">Performance and Tuning</span></span>
<span data-ttu-id="3420e-333">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="3420e-333">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
