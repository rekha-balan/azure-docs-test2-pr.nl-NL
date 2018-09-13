---
title: Move data from MongoDB using Data Factory | Microsoft Docs
description: Learn about how to move data from MongoDB database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/13/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 7c6751a0432d66aee0ff3056b212dc1b348e333f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857197"
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="f64ba-103">Move data From MongoDB using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f64ba-103">Move data From MongoDB using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-on-premises-mongodb-connector.md)
> * [Version 2 (current version)](../connector-mongodb.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [MongoDB connector in V2](../connector-mongodb.md).


<span data-ttu-id="f64ba-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="f64ba-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span></span> <span data-ttu-id="f64ba-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="f64ba-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="f64ba-110">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f64ba-110">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span></span> <span data-ttu-id="f64ba-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="f64ba-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="f64ba-112">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span><span class="sxs-lookup"><span data-stu-id="f64ba-112">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f64ba-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f64ba-113">Prerequisites</span></span>
<span data-ttu-id="f64ba-114">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span><span class="sxs-lookup"><span data-stu-id="f64ba-114">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span></span>

- <span data-ttu-id="f64ba-115">Supported MongoDB versions are:  2.4, 2.6, 3.0, 3.2, 3.4 and 3.6.</span><span class="sxs-lookup"><span data-stu-id="f64ba-115">Supported MongoDB versions are:  2.4, 2.6, 3.0, 3.2, 3.4 and 3.6.</span></span>
- <span data-ttu-id="f64ba-116">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span><span class="sxs-lookup"><span data-stu-id="f64ba-116">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="f64ba-117">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span><span class="sxs-lookup"><span data-stu-id="f64ba-117">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="f64ba-118">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f64ba-118">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="f64ba-119">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span><span class="sxs-lookup"><span data-stu-id="f64ba-119">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

    <span data-ttu-id="f64ba-120">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f64ba-120">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span></span>

    > [!NOTE]
    > You need to use the gateway to connect to MongoDB even if it is hosted in Azure IaaS VMs. If you are trying to connect to an instance of MongoDB hosted in cloud, you can also install the gateway instance in the IaaS VM.

## <a name="getting-started"></a><span data-ttu-id="f64ba-123">Getting started</span><span class="sxs-lookup"><span data-stu-id="f64ba-123">Getting started</span></span>
<span data-ttu-id="f64ba-124">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="f64ba-124">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="f64ba-125">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="f64ba-125">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f64ba-126">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="f64ba-126">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="f64ba-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="f64ba-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f64ba-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="f64ba-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f64ba-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="f64ba-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="f64ba-130">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f64ba-130">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="f64ba-131">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="f64ba-131">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="f64ba-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="f64ba-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f64ba-133">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="f64ba-133">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="f64ba-134">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="f64ba-134">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="f64ba-135">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="f64ba-135">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="f64ba-136">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span><span class="sxs-lookup"><span data-stu-id="f64ba-136">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f64ba-137">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f64ba-137">Linked service properties</span></span>
<span data-ttu-id="f64ba-138">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span><span class="sxs-lookup"><span data-stu-id="f64ba-138">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="f64ba-139">Property</span><span class="sxs-lookup"><span data-stu-id="f64ba-139">Property</span></span> | <span data-ttu-id="f64ba-140">Description</span><span class="sxs-lookup"><span data-stu-id="f64ba-140">Description</span></span> | <span data-ttu-id="f64ba-141">Required</span><span class="sxs-lookup"><span data-stu-id="f64ba-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f64ba-142">type</span><span class="sxs-lookup"><span data-stu-id="f64ba-142">type</span></span> |<span data-ttu-id="f64ba-143">The type property must be set to: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="f64ba-143">The type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="f64ba-144">Yes</span><span class="sxs-lookup"><span data-stu-id="f64ba-144">Yes</span></span> |
| <span data-ttu-id="f64ba-145">server</span><span class="sxs-lookup"><span data-stu-id="f64ba-145">server</span></span> |<span data-ttu-id="f64ba-146">IP address or host name of the MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="f64ba-146">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="f64ba-147">Yes</span><span class="sxs-lookup"><span data-stu-id="f64ba-147">Yes</span></span> |
| <span data-ttu-id="f64ba-148">port</span><span class="sxs-lookup"><span data-stu-id="f64ba-148">port</span></span> |<span data-ttu-id="f64ba-149">TCP port that the MongoDB server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="f64ba-149">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="f64ba-150">Optional, default value: 27017</span><span class="sxs-lookup"><span data-stu-id="f64ba-150">Optional, default value: 27017</span></span> |
| <span data-ttu-id="f64ba-151">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f64ba-151">authenticationType</span></span> |<span data-ttu-id="f64ba-152">Basic, or Anonymous.</span><span class="sxs-lookup"><span data-stu-id="f64ba-152">Basic, or Anonymous.</span></span> |<span data-ttu-id="f64ba-153">Yes</span><span class="sxs-lookup"><span data-stu-id="f64ba-153">Yes</span></span> |
| <span data-ttu-id="f64ba-154">username</span><span class="sxs-lookup"><span data-stu-id="f64ba-154">username</span></span> |<span data-ttu-id="f64ba-155">User account to access MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f64ba-155">User account to access MongoDB.</span></span> |<span data-ttu-id="f64ba-156">Yes (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="f64ba-156">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="f64ba-157">password</span><span class="sxs-lookup"><span data-stu-id="f64ba-157">password</span></span> |<span data-ttu-id="f64ba-158">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="f64ba-158">Password for the user.</span></span> |<span data-ttu-id="f64ba-159">Yes (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="f64ba-159">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="f64ba-160">authSource</span><span class="sxs-lookup"><span data-stu-id="f64ba-160">authSource</span></span> |<span data-ttu-id="f64ba-161">Name of the MongoDB database that you want to use to check your credentials for authentication.</span><span class="sxs-lookup"><span data-stu-id="f64ba-161">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="f64ba-162">Optional (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="f64ba-162">Optional (if basic authentication is used).</span></span> <span data-ttu-id="f64ba-163">default: uses the admin account and the database specified using databaseName property.</span><span class="sxs-lookup"><span data-stu-id="f64ba-163">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="f64ba-164">databaseName</span><span class="sxs-lookup"><span data-stu-id="f64ba-164">databaseName</span></span> |<span data-ttu-id="f64ba-165">Name of the MongoDB database that you want to access.</span><span class="sxs-lookup"><span data-stu-id="f64ba-165">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="f64ba-166">Yes</span><span class="sxs-lookup"><span data-stu-id="f64ba-166">Yes</span></span> |
| <span data-ttu-id="f64ba-167">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f64ba-167">gatewayName</span></span> |<span data-ttu-id="f64ba-168">Name of the gateway that accesses the data store.</span><span class="sxs-lookup"><span data-stu-id="f64ba-168">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="f64ba-169">Yes</span><span class="sxs-lookup"><span data-stu-id="f64ba-169">Yes</span></span> |
| <span data-ttu-id="f64ba-170">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="f64ba-170">encryptedCredential</span></span> |<span data-ttu-id="f64ba-171">Credential encrypted by gateway.</span><span class="sxs-lookup"><span data-stu-id="f64ba-171">Credential encrypted by gateway.</span></span> |<span data-ttu-id="f64ba-172">Optional</span><span class="sxs-lookup"><span data-stu-id="f64ba-172">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="f64ba-173">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f64ba-173">Dataset properties</span></span>
<span data-ttu-id="f64ba-174">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="f64ba-174">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f64ba-175">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="f64ba-175">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f64ba-176">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="f64ba-176">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f64ba-177">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="f64ba-177">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span></span>

| <span data-ttu-id="f64ba-178">Property</span><span class="sxs-lookup"><span data-stu-id="f64ba-178">Property</span></span> | <span data-ttu-id="f64ba-179">Description</span><span class="sxs-lookup"><span data-stu-id="f64ba-179">Description</span></span> | <span data-ttu-id="f64ba-180">Required</span><span class="sxs-lookup"><span data-stu-id="f64ba-180">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f64ba-181">collectionName</span><span class="sxs-lookup"><span data-stu-id="f64ba-181">collectionName</span></span> |<span data-ttu-id="f64ba-182">Name of the collection in MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="f64ba-182">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="f64ba-183">Yes</span><span class="sxs-lookup"><span data-stu-id="f64ba-183">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f64ba-184">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f64ba-184">Copy activity properties</span></span>
<span data-ttu-id="f64ba-185">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="f64ba-185">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f64ba-186">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="f64ba-186">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="f64ba-187">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="f64ba-187">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="f64ba-188">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="f64ba-188">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="f64ba-189">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="f64ba-189">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="f64ba-190">Property</span><span class="sxs-lookup"><span data-stu-id="f64ba-190">Property</span></span> | <span data-ttu-id="f64ba-191">Description</span><span class="sxs-lookup"><span data-stu-id="f64ba-191">Description</span></span> | <span data-ttu-id="f64ba-192">Allowed values</span><span class="sxs-lookup"><span data-stu-id="f64ba-192">Allowed values</span></span> | <span data-ttu-id="f64ba-193">Required</span><span class="sxs-lookup"><span data-stu-id="f64ba-193">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f64ba-194">query</span><span class="sxs-lookup"><span data-stu-id="f64ba-194">query</span></span> |<span data-ttu-id="f64ba-195">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="f64ba-195">Use the custom query to read data.</span></span> |<span data-ttu-id="f64ba-196">SQL-92 query string.</span><span class="sxs-lookup"><span data-stu-id="f64ba-196">SQL-92 query string.</span></span> <span data-ttu-id="f64ba-197">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="f64ba-197">For example: select \* from MyTable.</span></span> |<span data-ttu-id="f64ba-198">No (if **collectionName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="f64ba-198">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-to-azure-blob"></a><span data-ttu-id="f64ba-199">JSON example: Copy data from MongoDB to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="f64ba-199">JSON example: Copy data from MongoDB to Azure Blob</span></span>
<span data-ttu-id="f64ba-200">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f64ba-200">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f64ba-201">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f64ba-201">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span></span> <span data-ttu-id="f64ba-202">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f64ba-202">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="f64ba-203">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="f64ba-203">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="f64ba-204">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f64ba-204">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="f64ba-205">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f64ba-205">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f64ba-206">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f64ba-206">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="f64ba-207">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f64ba-207">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f64ba-208">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f64ba-208">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f64ba-209">The sample copies data from a query result in MongoDB database to a blob every hour.</span><span class="sxs-lookup"><span data-stu-id="f64ba-209">The sample copies data from a query result in MongoDB database to a blob every hour.</span></span> <span data-ttu-id="f64ba-210">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="f64ba-210">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f64ba-211">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span><span class="sxs-lookup"><span data-stu-id="f64ba-211">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="f64ba-212">**MongoDB linked service:**</span><span class="sxs-lookup"><span data-stu-id="f64ba-212">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",  
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="f64ba-213">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="f64ba-213">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="f64ba-214">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f64ba-214">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="f64ba-215">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="f64ba-215">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f64ba-216">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f64ba-216">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f64ba-217">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="f64ba-217">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f64ba-218">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="f64ba-218">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="f64ba-219">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="f64ba-219">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="f64ba-220">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="f64ba-220">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f64ba-221">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f64ba-221">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f64ba-222">The SQL query specified for the **query** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="f64ba-222">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="f64ba-223">Schema by Data Factory</span><span class="sxs-lookup"><span data-stu-id="f64ba-223">Schema by Data Factory</span></span>
<span data-ttu-id="f64ba-224">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span><span class="sxs-lookup"><span data-stu-id="f64ba-224">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span></span> <span data-ttu-id="f64ba-225">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span><span class="sxs-lookup"><span data-stu-id="f64ba-225">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="f64ba-226">Type mapping for MongoDB</span><span class="sxs-lookup"><span data-stu-id="f64ba-226">Type mapping for MongoDB</span></span>
<span data-ttu-id="f64ba-227">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="f64ba-227">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="f64ba-228">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="f64ba-228">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f64ba-229">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="f64ba-229">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f64ba-230">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span><span class="sxs-lookup"><span data-stu-id="f64ba-230">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span></span>

| <span data-ttu-id="f64ba-231">MongoDB type</span><span class="sxs-lookup"><span data-stu-id="f64ba-231">MongoDB type</span></span> | <span data-ttu-id="f64ba-232">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="f64ba-232">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="f64ba-233">Binary</span><span class="sxs-lookup"><span data-stu-id="f64ba-233">Binary</span></span> |<span data-ttu-id="f64ba-234">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f64ba-234">Byte[]</span></span> |
| <span data-ttu-id="f64ba-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="f64ba-235">Boolean</span></span> |<span data-ttu-id="f64ba-236">Boolean</span><span class="sxs-lookup"><span data-stu-id="f64ba-236">Boolean</span></span> |
| <span data-ttu-id="f64ba-237">Date</span><span class="sxs-lookup"><span data-stu-id="f64ba-237">Date</span></span> |<span data-ttu-id="f64ba-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="f64ba-238">DateTime</span></span> |
| <span data-ttu-id="f64ba-239">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="f64ba-239">NumberDouble</span></span> |<span data-ttu-id="f64ba-240">Double</span><span class="sxs-lookup"><span data-stu-id="f64ba-240">Double</span></span> |
| <span data-ttu-id="f64ba-241">NumberInt</span><span class="sxs-lookup"><span data-stu-id="f64ba-241">NumberInt</span></span> |<span data-ttu-id="f64ba-242">Int32</span><span class="sxs-lookup"><span data-stu-id="f64ba-242">Int32</span></span> |
| <span data-ttu-id="f64ba-243">NumberLong</span><span class="sxs-lookup"><span data-stu-id="f64ba-243">NumberLong</span></span> |<span data-ttu-id="f64ba-244">Int64</span><span class="sxs-lookup"><span data-stu-id="f64ba-244">Int64</span></span> |
| <span data-ttu-id="f64ba-245">ObjectID</span><span class="sxs-lookup"><span data-stu-id="f64ba-245">ObjectID</span></span> |<span data-ttu-id="f64ba-246">String</span><span class="sxs-lookup"><span data-stu-id="f64ba-246">String</span></span> |
| <span data-ttu-id="f64ba-247">String</span><span class="sxs-lookup"><span data-stu-id="f64ba-247">String</span></span> |<span data-ttu-id="f64ba-248">String</span><span class="sxs-lookup"><span data-stu-id="f64ba-248">String</span></span> |
| <span data-ttu-id="f64ba-249">UUID</span><span class="sxs-lookup"><span data-stu-id="f64ba-249">UUID</span></span> |<span data-ttu-id="f64ba-250">Guid</span><span class="sxs-lookup"><span data-stu-id="f64ba-250">Guid</span></span> |
| <span data-ttu-id="f64ba-251">Object</span><span class="sxs-lookup"><span data-stu-id="f64ba-251">Object</span></span> |<span data-ttu-id="f64ba-252">Renormalized into flatten columns with “_” as nested separator</span><span class="sxs-lookup"><span data-stu-id="f64ba-252">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.

<span data-ttu-id="f64ba-254">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span><span class="sxs-lookup"><span data-stu-id="f64ba-254">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="f64ba-255">Support for complex types using virtual tables</span><span class="sxs-lookup"><span data-stu-id="f64ba-255">Support for complex types using virtual tables</span></span>
<span data-ttu-id="f64ba-256">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="f64ba-256">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="f64ba-257">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span><span class="sxs-lookup"><span data-stu-id="f64ba-257">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="f64ba-258">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span><span class="sxs-lookup"><span data-stu-id="f64ba-258">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="f64ba-259">A **base table**, which contains the same data as the real table except for the complex type columns.</span><span class="sxs-lookup"><span data-stu-id="f64ba-259">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="f64ba-260">The base table uses the same name as the real table that it represents.</span><span class="sxs-lookup"><span data-stu-id="f64ba-260">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="f64ba-261">A **virtual table** for each complex type column, which expands the nested data.</span><span class="sxs-lookup"><span data-stu-id="f64ba-261">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="f64ba-262">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span><span class="sxs-lookup"><span data-stu-id="f64ba-262">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span></span>

<span data-ttu-id="f64ba-263">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span><span class="sxs-lookup"><span data-stu-id="f64ba-263">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="f64ba-264">See Example section below details.</span><span class="sxs-lookup"><span data-stu-id="f64ba-264">See Example section below details.</span></span> <span data-ttu-id="f64ba-265">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span><span class="sxs-lookup"><span data-stu-id="f64ba-265">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

<span data-ttu-id="f64ba-266">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span><span class="sxs-lookup"><span data-stu-id="f64ba-266">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="f64ba-267">You can also construct a query in the Copy Wizard and validate to see the result.</span><span class="sxs-lookup"><span data-stu-id="f64ba-267">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="f64ba-268">Example</span><span class="sxs-lookup"><span data-stu-id="f64ba-268">Example</span></span>
<span data-ttu-id="f64ba-269">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span><span class="sxs-lookup"><span data-stu-id="f64ba-269">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="f64ba-270">_id</span><span class="sxs-lookup"><span data-stu-id="f64ba-270">_id</span></span> | <span data-ttu-id="f64ba-271">Customer Name</span><span class="sxs-lookup"><span data-stu-id="f64ba-271">Customer Name</span></span> | <span data-ttu-id="f64ba-272">Invoices</span><span class="sxs-lookup"><span data-stu-id="f64ba-272">Invoices</span></span> | <span data-ttu-id="f64ba-273">Service Level</span><span class="sxs-lookup"><span data-stu-id="f64ba-273">Service Level</span></span> | <span data-ttu-id="f64ba-274">Ratings</span><span class="sxs-lookup"><span data-stu-id="f64ba-274">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f64ba-275">1111</span><span class="sxs-lookup"><span data-stu-id="f64ba-275">1111</span></span> |<span data-ttu-id="f64ba-276">ABC</span><span class="sxs-lookup"><span data-stu-id="f64ba-276">ABC</span></span> |<span data-ttu-id="f64ba-277">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="f64ba-277">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="f64ba-278">Silver</span><span class="sxs-lookup"><span data-stu-id="f64ba-278">Silver</span></span> |<span data-ttu-id="f64ba-279">[5,6]</span><span class="sxs-lookup"><span data-stu-id="f64ba-279">[5,6]</span></span> |
| <span data-ttu-id="f64ba-280">2222</span><span class="sxs-lookup"><span data-stu-id="f64ba-280">2222</span></span> |<span data-ttu-id="f64ba-281">XYZ</span><span class="sxs-lookup"><span data-stu-id="f64ba-281">XYZ</span></span> |<span data-ttu-id="f64ba-282">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="f64ba-282">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="f64ba-283">Gold</span><span class="sxs-lookup"><span data-stu-id="f64ba-283">Gold</span></span> |<span data-ttu-id="f64ba-284">[1,2]</span><span class="sxs-lookup"><span data-stu-id="f64ba-284">[1,2]</span></span> |

<span data-ttu-id="f64ba-285">The driver would generate multiple virtual tables to represent this single table.</span><span class="sxs-lookup"><span data-stu-id="f64ba-285">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="f64ba-286">The first virtual table is the base table named “ExampleTable”, shown below.</span><span class="sxs-lookup"><span data-stu-id="f64ba-286">The first virtual table is the base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="f64ba-287">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span><span class="sxs-lookup"><span data-stu-id="f64ba-287">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="f64ba-288">_id</span><span class="sxs-lookup"><span data-stu-id="f64ba-288">_id</span></span> | <span data-ttu-id="f64ba-289">Customer Name</span><span class="sxs-lookup"><span data-stu-id="f64ba-289">Customer Name</span></span> | <span data-ttu-id="f64ba-290">Service Level</span><span class="sxs-lookup"><span data-stu-id="f64ba-290">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f64ba-291">1111</span><span class="sxs-lookup"><span data-stu-id="f64ba-291">1111</span></span> |<span data-ttu-id="f64ba-292">ABC</span><span class="sxs-lookup"><span data-stu-id="f64ba-292">ABC</span></span> |<span data-ttu-id="f64ba-293">Silver</span><span class="sxs-lookup"><span data-stu-id="f64ba-293">Silver</span></span> |
| <span data-ttu-id="f64ba-294">2222</span><span class="sxs-lookup"><span data-stu-id="f64ba-294">2222</span></span> |<span data-ttu-id="f64ba-295">XYZ</span><span class="sxs-lookup"><span data-stu-id="f64ba-295">XYZ</span></span> |<span data-ttu-id="f64ba-296">Gold</span><span class="sxs-lookup"><span data-stu-id="f64ba-296">Gold</span></span> |

<span data-ttu-id="f64ba-297">The following tables show the virtual tables that represent the original arrays in the example.</span><span class="sxs-lookup"><span data-stu-id="f64ba-297">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="f64ba-298">These tables contain the following:</span><span class="sxs-lookup"><span data-stu-id="f64ba-298">These tables contain the following:</span></span>

* <span data-ttu-id="f64ba-299">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span><span class="sxs-lookup"><span data-stu-id="f64ba-299">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="f64ba-300">An indication of the position of the data within the original array</span><span class="sxs-lookup"><span data-stu-id="f64ba-300">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="f64ba-301">The expanded data for each element within the array</span><span class="sxs-lookup"><span data-stu-id="f64ba-301">The expanded data for each element within the array</span></span>

<span data-ttu-id="f64ba-302">Table “ExampleTable_Invoices”:</span><span class="sxs-lookup"><span data-stu-id="f64ba-302">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="f64ba-303">_id</span><span class="sxs-lookup"><span data-stu-id="f64ba-303">_id</span></span> | <span data-ttu-id="f64ba-304">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="f64ba-304">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="f64ba-305">invoice_id</span><span class="sxs-lookup"><span data-stu-id="f64ba-305">invoice_id</span></span> | <span data-ttu-id="f64ba-306">item</span><span class="sxs-lookup"><span data-stu-id="f64ba-306">item</span></span> | <span data-ttu-id="f64ba-307">price</span><span class="sxs-lookup"><span data-stu-id="f64ba-307">price</span></span> | <span data-ttu-id="f64ba-308">Discount</span><span class="sxs-lookup"><span data-stu-id="f64ba-308">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f64ba-309">1111</span><span class="sxs-lookup"><span data-stu-id="f64ba-309">1111</span></span> |<span data-ttu-id="f64ba-310">0</span><span class="sxs-lookup"><span data-stu-id="f64ba-310">0</span></span> |<span data-ttu-id="f64ba-311">123</span><span class="sxs-lookup"><span data-stu-id="f64ba-311">123</span></span> |<span data-ttu-id="f64ba-312">toaster</span><span class="sxs-lookup"><span data-stu-id="f64ba-312">toaster</span></span> |<span data-ttu-id="f64ba-313">456</span><span class="sxs-lookup"><span data-stu-id="f64ba-313">456</span></span> |<span data-ttu-id="f64ba-314">0.2</span><span class="sxs-lookup"><span data-stu-id="f64ba-314">0.2</span></span> |
| <span data-ttu-id="f64ba-315">1111</span><span class="sxs-lookup"><span data-stu-id="f64ba-315">1111</span></span> |<span data-ttu-id="f64ba-316">1</span><span class="sxs-lookup"><span data-stu-id="f64ba-316">1</span></span> |<span data-ttu-id="f64ba-317">124</span><span class="sxs-lookup"><span data-stu-id="f64ba-317">124</span></span> |<span data-ttu-id="f64ba-318">oven</span><span class="sxs-lookup"><span data-stu-id="f64ba-318">oven</span></span> |<span data-ttu-id="f64ba-319">1235</span><span class="sxs-lookup"><span data-stu-id="f64ba-319">1235</span></span> |<span data-ttu-id="f64ba-320">0.2</span><span class="sxs-lookup"><span data-stu-id="f64ba-320">0.2</span></span> |
| <span data-ttu-id="f64ba-321">2222</span><span class="sxs-lookup"><span data-stu-id="f64ba-321">2222</span></span> |<span data-ttu-id="f64ba-322">0</span><span class="sxs-lookup"><span data-stu-id="f64ba-322">0</span></span> |<span data-ttu-id="f64ba-323">135</span><span class="sxs-lookup"><span data-stu-id="f64ba-323">135</span></span> |<span data-ttu-id="f64ba-324">fridge</span><span class="sxs-lookup"><span data-stu-id="f64ba-324">fridge</span></span> |<span data-ttu-id="f64ba-325">12543</span><span class="sxs-lookup"><span data-stu-id="f64ba-325">12543</span></span> |<span data-ttu-id="f64ba-326">0.0</span><span class="sxs-lookup"><span data-stu-id="f64ba-326">0.0</span></span> |

<span data-ttu-id="f64ba-327">Table “ExampleTable_Ratings”:</span><span class="sxs-lookup"><span data-stu-id="f64ba-327">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="f64ba-328">_id</span><span class="sxs-lookup"><span data-stu-id="f64ba-328">_id</span></span> | <span data-ttu-id="f64ba-329">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="f64ba-329">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="f64ba-330">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="f64ba-330">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f64ba-331">1111</span><span class="sxs-lookup"><span data-stu-id="f64ba-331">1111</span></span> |<span data-ttu-id="f64ba-332">0</span><span class="sxs-lookup"><span data-stu-id="f64ba-332">0</span></span> |<span data-ttu-id="f64ba-333">5</span><span class="sxs-lookup"><span data-stu-id="f64ba-333">5</span></span> |
| <span data-ttu-id="f64ba-334">1111</span><span class="sxs-lookup"><span data-stu-id="f64ba-334">1111</span></span> |<span data-ttu-id="f64ba-335">1</span><span class="sxs-lookup"><span data-stu-id="f64ba-335">1</span></span> |<span data-ttu-id="f64ba-336">6</span><span class="sxs-lookup"><span data-stu-id="f64ba-336">6</span></span> |
| <span data-ttu-id="f64ba-337">2222</span><span class="sxs-lookup"><span data-stu-id="f64ba-337">2222</span></span> |<span data-ttu-id="f64ba-338">0</span><span class="sxs-lookup"><span data-stu-id="f64ba-338">0</span></span> |<span data-ttu-id="f64ba-339">1</span><span class="sxs-lookup"><span data-stu-id="f64ba-339">1</span></span> |
| <span data-ttu-id="f64ba-340">2222</span><span class="sxs-lookup"><span data-stu-id="f64ba-340">2222</span></span> |<span data-ttu-id="f64ba-341">1</span><span class="sxs-lookup"><span data-stu-id="f64ba-341">1</span></span> |<span data-ttu-id="f64ba-342">2</span><span class="sxs-lookup"><span data-stu-id="f64ba-342">2</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="f64ba-343">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="f64ba-343">Map source to sink columns</span></span>
<span data-ttu-id="f64ba-344">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f64ba-344">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="f64ba-345">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="f64ba-345">Repeatable read from relational sources</span></span>
<span data-ttu-id="f64ba-346">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="f64ba-346">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="f64ba-347">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="f64ba-347">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f64ba-348">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="f64ba-348">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f64ba-349">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="f64ba-349">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f64ba-350">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f64ba-350">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f64ba-351">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="f64ba-351">Performance and Tuning</span></span>
<span data-ttu-id="f64ba-352">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="f64ba-352">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f64ba-353">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f64ba-353">Next Steps</span></span>
<span data-ttu-id="f64ba-354">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span><span class="sxs-lookup"><span data-stu-id="f64ba-354">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span></span>
