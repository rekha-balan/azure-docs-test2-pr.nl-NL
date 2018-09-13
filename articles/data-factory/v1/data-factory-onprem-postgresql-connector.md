---
title: Move data From PostgreSQL using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from PostgreSQL Database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 189adf27795172bb08b52af1a9e3428d854a50a0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869424"
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="f70b0-103">Move data from PostgreSQL using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f70b0-103">Move data from PostgreSQL using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-onprem-postgresql-connector.md)
> * [Version 2 (current version)](../connector-postgresql.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [PostgreSQL connector in V2](../connector-postgresql.md).


<span data-ttu-id="f70b0-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="f70b0-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="f70b0-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="f70b0-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="f70b0-110">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f70b0-110">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span></span> <span data-ttu-id="f70b0-111">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f70b0-111">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f70b0-112">Data factory currently supports moving data from a PostgreSQL database to other data stores, but not for moving data from other data stores to an PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="f70b0-112">Data factory currently supports moving data from a PostgreSQL database to other data stores, but not for moving data from other data stores to an PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f70b0-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f70b0-113">Prerequisites</span></span>

<span data-ttu-id="f70b0-114">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f70b0-114">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="f70b0-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span><span class="sxs-lookup"><span data-stu-id="f70b0-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="f70b0-116">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="f70b0-116">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="f70b0-117">You can install gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="f70b0-117">You can install gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.

## <a name="supported-versions-and-installation"></a><span data-ttu-id="f70b0-119">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="f70b0-119">Supported versions and installation</span></span>
<span data-ttu-id="f70b0-120">For Data Management Gateway to connect to the PostgreSQL Database, install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) with version between 2.0.12 and 3.1.9 on the same system as the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f70b0-120">For Data Management Gateway to connect to the PostgreSQL Database, install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) with version between 2.0.12 and 3.1.9 on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="f70b0-121">PostgreSQL version 7.4 and above is supported.</span><span class="sxs-lookup"><span data-stu-id="f70b0-121">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f70b0-122">Getting started</span><span class="sxs-lookup"><span data-stu-id="f70b0-122">Getting started</span></span>
<span data-ttu-id="f70b0-123">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="f70b0-123">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="f70b0-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="f70b0-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f70b0-125">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="f70b0-125">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="f70b0-126">You can also use the following tools to create a pipeline:</span><span class="sxs-lookup"><span data-stu-id="f70b0-126">You can also use the following tools to create a pipeline:</span></span> 
    - <span data-ttu-id="f70b0-127">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f70b0-127">Azure portal</span></span>
    - <span data-ttu-id="f70b0-128">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f70b0-128">Visual Studio</span></span>
    - <span data-ttu-id="f70b0-129">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f70b0-129">Azure PowerShell</span></span>
    - <span data-ttu-id="f70b0-130">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="f70b0-130">Azure Resource Manager template</span></span>
    - <span data-ttu-id="f70b0-131">.NET API</span><span class="sxs-lookup"><span data-stu-id="f70b0-131">.NET API</span></span>
    - <span data-ttu-id="f70b0-132">REST API</span><span class="sxs-lookup"><span data-stu-id="f70b0-132">REST API</span></span>

     <span data-ttu-id="f70b0-133">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="f70b0-133">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f70b0-134">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="f70b0-134">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="f70b0-135">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f70b0-135">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="f70b0-136">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="f70b0-136">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="f70b0-137">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="f70b0-137">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f70b0-138">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="f70b0-138">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="f70b0-139">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="f70b0-139">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="f70b0-140">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="f70b0-140">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="f70b0-141">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span><span class="sxs-lookup"><span data-stu-id="f70b0-141">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f70b0-142">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f70b0-142">Linked service properties</span></span>
<span data-ttu-id="f70b0-143">The following table provides description for JSON elements specific to PostgreSQL linked service.</span><span class="sxs-lookup"><span data-stu-id="f70b0-143">The following table provides description for JSON elements specific to PostgreSQL linked service.</span></span>

| <span data-ttu-id="f70b0-144">Property</span><span class="sxs-lookup"><span data-stu-id="f70b0-144">Property</span></span> | <span data-ttu-id="f70b0-145">Description</span><span class="sxs-lookup"><span data-stu-id="f70b0-145">Description</span></span> | <span data-ttu-id="f70b0-146">Required</span><span class="sxs-lookup"><span data-stu-id="f70b0-146">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f70b0-147">type</span><span class="sxs-lookup"><span data-stu-id="f70b0-147">type</span></span> |<span data-ttu-id="f70b0-148">The type property must be set to: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="f70b0-148">The type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="f70b0-149">Yes</span><span class="sxs-lookup"><span data-stu-id="f70b0-149">Yes</span></span> |
| <span data-ttu-id="f70b0-150">server</span><span class="sxs-lookup"><span data-stu-id="f70b0-150">server</span></span> |<span data-ttu-id="f70b0-151">Name of the PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="f70b0-151">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="f70b0-152">Yes</span><span class="sxs-lookup"><span data-stu-id="f70b0-152">Yes</span></span> |
| <span data-ttu-id="f70b0-153">database</span><span class="sxs-lookup"><span data-stu-id="f70b0-153">database</span></span> |<span data-ttu-id="f70b0-154">Name of the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="f70b0-154">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="f70b0-155">Yes</span><span class="sxs-lookup"><span data-stu-id="f70b0-155">Yes</span></span> |
| <span data-ttu-id="f70b0-156">schema</span><span class="sxs-lookup"><span data-stu-id="f70b0-156">schema</span></span> |<span data-ttu-id="f70b0-157">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="f70b0-157">Name of the schema in the database.</span></span> <span data-ttu-id="f70b0-158">The schema name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="f70b0-158">The schema name is case-sensitive.</span></span> |<span data-ttu-id="f70b0-159">No</span><span class="sxs-lookup"><span data-stu-id="f70b0-159">No</span></span> |
| <span data-ttu-id="f70b0-160">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f70b0-160">authenticationType</span></span> |<span data-ttu-id="f70b0-161">Type of authentication used to connect to the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="f70b0-161">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="f70b0-162">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="f70b0-162">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="f70b0-163">Yes</span><span class="sxs-lookup"><span data-stu-id="f70b0-163">Yes</span></span> |
| <span data-ttu-id="f70b0-164">username</span><span class="sxs-lookup"><span data-stu-id="f70b0-164">username</span></span> |<span data-ttu-id="f70b0-165">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="f70b0-165">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="f70b0-166">No</span><span class="sxs-lookup"><span data-stu-id="f70b0-166">No</span></span> |
| <span data-ttu-id="f70b0-167">password</span><span class="sxs-lookup"><span data-stu-id="f70b0-167">password</span></span> |<span data-ttu-id="f70b0-168">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="f70b0-168">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="f70b0-169">No</span><span class="sxs-lookup"><span data-stu-id="f70b0-169">No</span></span> |
| <span data-ttu-id="f70b0-170">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f70b0-170">gatewayName</span></span> |<span data-ttu-id="f70b0-171">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="f70b0-171">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="f70b0-172">Yes</span><span class="sxs-lookup"><span data-stu-id="f70b0-172">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="f70b0-173">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f70b0-173">Dataset properties</span></span>
<span data-ttu-id="f70b0-174">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="f70b0-174">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f70b0-175">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span><span class="sxs-lookup"><span data-stu-id="f70b0-175">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="f70b0-176">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="f70b0-176">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f70b0-177">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span><span class="sxs-lookup"><span data-stu-id="f70b0-177">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span></span>

| <span data-ttu-id="f70b0-178">Property</span><span class="sxs-lookup"><span data-stu-id="f70b0-178">Property</span></span> | <span data-ttu-id="f70b0-179">Description</span><span class="sxs-lookup"><span data-stu-id="f70b0-179">Description</span></span> | <span data-ttu-id="f70b0-180">Required</span><span class="sxs-lookup"><span data-stu-id="f70b0-180">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f70b0-181">tableName</span><span class="sxs-lookup"><span data-stu-id="f70b0-181">tableName</span></span> |<span data-ttu-id="f70b0-182">Name of the table in the PostgreSQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="f70b0-182">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="f70b0-183">The tableName is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="f70b0-183">The tableName is case-sensitive.</span></span> |<span data-ttu-id="f70b0-184">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="f70b0-184">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f70b0-185">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f70b0-185">Copy activity properties</span></span>
<span data-ttu-id="f70b0-186">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="f70b0-186">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f70b0-187">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="f70b0-187">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="f70b0-188">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="f70b0-188">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="f70b0-189">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="f70b0-189">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="f70b0-190">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="f70b0-190">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="f70b0-191">Property</span><span class="sxs-lookup"><span data-stu-id="f70b0-191">Property</span></span> | <span data-ttu-id="f70b0-192">Description</span><span class="sxs-lookup"><span data-stu-id="f70b0-192">Description</span></span> | <span data-ttu-id="f70b0-193">Allowed values</span><span class="sxs-lookup"><span data-stu-id="f70b0-193">Allowed values</span></span> | <span data-ttu-id="f70b0-194">Required</span><span class="sxs-lookup"><span data-stu-id="f70b0-194">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f70b0-195">query</span><span class="sxs-lookup"><span data-stu-id="f70b0-195">query</span></span> |<span data-ttu-id="f70b0-196">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="f70b0-196">Use the custom query to read data.</span></span> |<span data-ttu-id="f70b0-197">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="f70b0-197">SQL query string.</span></span> <span data-ttu-id="f70b0-198">For example: `"query": "select * from \"MySchema\".\"MyTable\""`.</span><span class="sxs-lookup"><span data-stu-id="f70b0-198">For example: `"query": "select * from \"MySchema\".\"MyTable\""`.</span></span> |<span data-ttu-id="f70b0-199">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="f70b0-199">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> Schema and table names are case-sensitive. Enclose them in `""` (double quotes) in the query.  

<span data-ttu-id="f70b0-202">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f70b0-202">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-to-azure-blob"></a><span data-ttu-id="f70b0-203">JSON example: Copy data from PostgreSQL to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="f70b0-203">JSON example: Copy data from PostgreSQL to Azure Blob</span></span>
<span data-ttu-id="f70b0-204">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f70b0-204">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f70b0-205">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f70b0-205">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span></span> <span data-ttu-id="f70b0-206">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f70b0-206">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> This sample provides JSON snippets. It does not include step-by-step instructions for creating the data factory. See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.

<span data-ttu-id="f70b0-210">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="f70b0-210">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="f70b0-211">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f70b0-211">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="f70b0-212">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f70b0-212">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f70b0-213">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f70b0-213">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="f70b0-214">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f70b0-214">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f70b0-215">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f70b0-215">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f70b0-216">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="f70b0-216">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span></span> <span data-ttu-id="f70b0-217">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="f70b0-217">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f70b0-218">As a first step, set up the data management gateway.</span><span class="sxs-lookup"><span data-stu-id="f70b0-218">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="f70b0-219">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="f70b0-219">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f70b0-220">**PostgreSQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="f70b0-220">**PostgreSQL linked service:**</span></span>

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
<span data-ttu-id="f70b0-221">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="f70b0-221">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="f70b0-222">**PostgreSQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="f70b0-222">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="f70b0-223">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span><span class="sxs-lookup"><span data-stu-id="f70b0-223">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="f70b0-224">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f70b0-224">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="f70b0-225">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="f70b0-225">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f70b0-226">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f70b0-226">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f70b0-227">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="f70b0-227">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f70b0-228">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="f70b0-228">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="f70b0-229">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="f70b0-229">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="f70b0-230">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span><span class="sxs-lookup"><span data-stu-id="f70b0-230">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="f70b0-231">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f70b0-231">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f70b0-232">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="f70b0-232">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span></span>

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
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="f70b0-233">Type mapping for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f70b0-233">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="f70b0-234">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="f70b0-234">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="f70b0-235">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="f70b0-235">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f70b0-236">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="f70b0-236">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f70b0-237">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span><span class="sxs-lookup"><span data-stu-id="f70b0-237">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span></span>

| <span data-ttu-id="f70b0-238">PostgreSQL Database type</span><span class="sxs-lookup"><span data-stu-id="f70b0-238">PostgreSQL Database type</span></span> | <span data-ttu-id="f70b0-239">PostgresSQL aliases</span><span class="sxs-lookup"><span data-stu-id="f70b0-239">PostgresSQL aliases</span></span> | <span data-ttu-id="f70b0-240">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="f70b0-240">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f70b0-241">abstime</span><span class="sxs-lookup"><span data-stu-id="f70b0-241">abstime</span></span> | |<span data-ttu-id="f70b0-242">Datetime</span><span class="sxs-lookup"><span data-stu-id="f70b0-242">Datetime</span></span> | &nbsp;
| <span data-ttu-id="f70b0-243">bigint</span><span class="sxs-lookup"><span data-stu-id="f70b0-243">bigint</span></span> |<span data-ttu-id="f70b0-244">int8</span><span class="sxs-lookup"><span data-stu-id="f70b0-244">int8</span></span> |<span data-ttu-id="f70b0-245">Int64</span><span class="sxs-lookup"><span data-stu-id="f70b0-245">Int64</span></span> |
| <span data-ttu-id="f70b0-246">bigserial</span><span class="sxs-lookup"><span data-stu-id="f70b0-246">bigserial</span></span> |<span data-ttu-id="f70b0-247">serial8</span><span class="sxs-lookup"><span data-stu-id="f70b0-247">serial8</span></span> |<span data-ttu-id="f70b0-248">Int64</span><span class="sxs-lookup"><span data-stu-id="f70b0-248">Int64</span></span> |
| <span data-ttu-id="f70b0-249">bit [(n)]</span><span class="sxs-lookup"><span data-stu-id="f70b0-249">bit [(n)]</span></span> | |<span data-ttu-id="f70b0-250">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-250">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="f70b0-251">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="f70b0-251">bit varying [ (n) ]</span></span> |<span data-ttu-id="f70b0-252">varbit</span><span class="sxs-lookup"><span data-stu-id="f70b0-252">varbit</span></span> |<span data-ttu-id="f70b0-253">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-253">Byte[], String</span></span> |
| <span data-ttu-id="f70b0-254">boolean</span><span class="sxs-lookup"><span data-stu-id="f70b0-254">boolean</span></span> |<span data-ttu-id="f70b0-255">bool</span><span class="sxs-lookup"><span data-stu-id="f70b0-255">bool</span></span> |<span data-ttu-id="f70b0-256">Boolean</span><span class="sxs-lookup"><span data-stu-id="f70b0-256">Boolean</span></span> |
| <span data-ttu-id="f70b0-257">box</span><span class="sxs-lookup"><span data-stu-id="f70b0-257">box</span></span> | |<span data-ttu-id="f70b0-258">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-258">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-259">bytea</span><span class="sxs-lookup"><span data-stu-id="f70b0-259">bytea</span></span> | |<span data-ttu-id="f70b0-260">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-260">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-261">character [(n)]</span><span class="sxs-lookup"><span data-stu-id="f70b0-261">character [(n)]</span></span> |<span data-ttu-id="f70b0-262">char [(n)]</span><span class="sxs-lookup"><span data-stu-id="f70b0-262">char [(n)]</span></span> |<span data-ttu-id="f70b0-263">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-263">String</span></span> |
| <span data-ttu-id="f70b0-264">character varying [(n)]</span><span class="sxs-lookup"><span data-stu-id="f70b0-264">character varying [(n)]</span></span> |<span data-ttu-id="f70b0-265">varchar [(n)]</span><span class="sxs-lookup"><span data-stu-id="f70b0-265">varchar [(n)]</span></span> |<span data-ttu-id="f70b0-266">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-266">String</span></span> |
| <span data-ttu-id="f70b0-267">cid</span><span class="sxs-lookup"><span data-stu-id="f70b0-267">cid</span></span> | |<span data-ttu-id="f70b0-268">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-268">String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-269">cidr</span><span class="sxs-lookup"><span data-stu-id="f70b0-269">cidr</span></span> | |<span data-ttu-id="f70b0-270">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-270">String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-271">circle</span><span class="sxs-lookup"><span data-stu-id="f70b0-271">circle</span></span> | |<span data-ttu-id="f70b0-272">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-272">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-273">date</span><span class="sxs-lookup"><span data-stu-id="f70b0-273">date</span></span> | |<span data-ttu-id="f70b0-274">Datetime</span><span class="sxs-lookup"><span data-stu-id="f70b0-274">Datetime</span></span> |&nbsp;
| <span data-ttu-id="f70b0-275">daterange</span><span class="sxs-lookup"><span data-stu-id="f70b0-275">daterange</span></span> | |<span data-ttu-id="f70b0-276">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-276">String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-277">double precision</span><span class="sxs-lookup"><span data-stu-id="f70b0-277">double precision</span></span> |<span data-ttu-id="f70b0-278">float8</span><span class="sxs-lookup"><span data-stu-id="f70b0-278">float8</span></span> |<span data-ttu-id="f70b0-279">Double</span><span class="sxs-lookup"><span data-stu-id="f70b0-279">Double</span></span> |
| <span data-ttu-id="f70b0-280">inet</span><span class="sxs-lookup"><span data-stu-id="f70b0-280">inet</span></span> | |<span data-ttu-id="f70b0-281">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-281">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-282">intarry</span><span class="sxs-lookup"><span data-stu-id="f70b0-282">intarry</span></span> | |<span data-ttu-id="f70b0-283">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-283">String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-284">int4range</span><span class="sxs-lookup"><span data-stu-id="f70b0-284">int4range</span></span> | |<span data-ttu-id="f70b0-285">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-285">String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-286">int8range</span><span class="sxs-lookup"><span data-stu-id="f70b0-286">int8range</span></span> | |<span data-ttu-id="f70b0-287">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-287">String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-288">integer</span><span class="sxs-lookup"><span data-stu-id="f70b0-288">integer</span></span> |<span data-ttu-id="f70b0-289">int, int4</span><span class="sxs-lookup"><span data-stu-id="f70b0-289">int, int4</span></span> |<span data-ttu-id="f70b0-290">Int32</span><span class="sxs-lookup"><span data-stu-id="f70b0-290">Int32</span></span> |
| <span data-ttu-id="f70b0-291">interval [fields] [(p)]</span><span class="sxs-lookup"><span data-stu-id="f70b0-291">interval [fields] [(p)]</span></span> | |<span data-ttu-id="f70b0-292">Timespan</span><span class="sxs-lookup"><span data-stu-id="f70b0-292">Timespan</span></span> |&nbsp;
| <span data-ttu-id="f70b0-293">json</span><span class="sxs-lookup"><span data-stu-id="f70b0-293">json</span></span> | |<span data-ttu-id="f70b0-294">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-294">String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-295">jsonb</span><span class="sxs-lookup"><span data-stu-id="f70b0-295">jsonb</span></span> | |<span data-ttu-id="f70b0-296">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f70b0-296">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="f70b0-297">line</span><span class="sxs-lookup"><span data-stu-id="f70b0-297">line</span></span> | |<span data-ttu-id="f70b0-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-299">lseg</span><span class="sxs-lookup"><span data-stu-id="f70b0-299">lseg</span></span> | |<span data-ttu-id="f70b0-300">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-300">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-301">macaddr</span><span class="sxs-lookup"><span data-stu-id="f70b0-301">macaddr</span></span> | |<span data-ttu-id="f70b0-302">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-302">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-303">money</span><span class="sxs-lookup"><span data-stu-id="f70b0-303">money</span></span> | |<span data-ttu-id="f70b0-304">Decimal</span><span class="sxs-lookup"><span data-stu-id="f70b0-304">Decimal</span></span> |&nbsp;
| <span data-ttu-id="f70b0-305">numeric [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="f70b0-305">numeric [(p, s)]</span></span> |<span data-ttu-id="f70b0-306">decimal [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="f70b0-306">decimal [(p, s)]</span></span> |<span data-ttu-id="f70b0-307">Decimal</span><span class="sxs-lookup"><span data-stu-id="f70b0-307">Decimal</span></span> |
| <span data-ttu-id="f70b0-308">numrange</span><span class="sxs-lookup"><span data-stu-id="f70b0-308">numrange</span></span> | |<span data-ttu-id="f70b0-309">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-309">String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-310">oid</span><span class="sxs-lookup"><span data-stu-id="f70b0-310">oid</span></span> | |<span data-ttu-id="f70b0-311">Int32</span><span class="sxs-lookup"><span data-stu-id="f70b0-311">Int32</span></span> |&nbsp;
| <span data-ttu-id="f70b0-312">path</span><span class="sxs-lookup"><span data-stu-id="f70b0-312">path</span></span> | |<span data-ttu-id="f70b0-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-314">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="f70b0-314">pg_lsn</span></span> | |<span data-ttu-id="f70b0-315">Int64</span><span class="sxs-lookup"><span data-stu-id="f70b0-315">Int64</span></span> |&nbsp;
| <span data-ttu-id="f70b0-316">point</span><span class="sxs-lookup"><span data-stu-id="f70b0-316">point</span></span> | |<span data-ttu-id="f70b0-317">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-317">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-318">polygon</span><span class="sxs-lookup"><span data-stu-id="f70b0-318">polygon</span></span> | |<span data-ttu-id="f70b0-319">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f70b0-319">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f70b0-320">real</span><span class="sxs-lookup"><span data-stu-id="f70b0-320">real</span></span> |<span data-ttu-id="f70b0-321">float4</span><span class="sxs-lookup"><span data-stu-id="f70b0-321">float4</span></span> |<span data-ttu-id="f70b0-322">Single</span><span class="sxs-lookup"><span data-stu-id="f70b0-322">Single</span></span> |
| <span data-ttu-id="f70b0-323">smallint</span><span class="sxs-lookup"><span data-stu-id="f70b0-323">smallint</span></span> |<span data-ttu-id="f70b0-324">int2</span><span class="sxs-lookup"><span data-stu-id="f70b0-324">int2</span></span> |<span data-ttu-id="f70b0-325">Int16</span><span class="sxs-lookup"><span data-stu-id="f70b0-325">Int16</span></span> |
| <span data-ttu-id="f70b0-326">smallserial</span><span class="sxs-lookup"><span data-stu-id="f70b0-326">smallserial</span></span> |<span data-ttu-id="f70b0-327">serial2</span><span class="sxs-lookup"><span data-stu-id="f70b0-327">serial2</span></span> |<span data-ttu-id="f70b0-328">Int16</span><span class="sxs-lookup"><span data-stu-id="f70b0-328">Int16</span></span> |
| <span data-ttu-id="f70b0-329">serial</span><span class="sxs-lookup"><span data-stu-id="f70b0-329">serial</span></span> |<span data-ttu-id="f70b0-330">serial4</span><span class="sxs-lookup"><span data-stu-id="f70b0-330">serial4</span></span> |<span data-ttu-id="f70b0-331">Int32</span><span class="sxs-lookup"><span data-stu-id="f70b0-331">Int32</span></span> |
| <span data-ttu-id="f70b0-332">text</span><span class="sxs-lookup"><span data-stu-id="f70b0-332">text</span></span> | |<span data-ttu-id="f70b0-333">String</span><span class="sxs-lookup"><span data-stu-id="f70b0-333">String</span></span> |&nbsp;

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="f70b0-334">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="f70b0-334">Map source to sink columns</span></span>
<span data-ttu-id="f70b0-335">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f70b0-335">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="f70b0-336">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="f70b0-336">Repeatable read from relational sources</span></span>
<span data-ttu-id="f70b0-337">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="f70b0-337">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="f70b0-338">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="f70b0-338">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f70b0-339">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="f70b0-339">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f70b0-340">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="f70b0-340">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f70b0-341">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f70b0-341">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f70b0-342">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="f70b0-342">Performance and Tuning</span></span>
<span data-ttu-id="f70b0-343">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="f70b0-343">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
