---
title: Move data from Cassandra using Data Factory | Microsoft Docs
description: Learn about how to move data from an on-premises Cassandra database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: jingwang
ms.openlocfilehash: 6a48c11508bdc7f6f6fbfe4a504172f9944c93c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563890"
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="af638-103">Move data from an on-premises Cassandra database using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af638-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="af638-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="af638-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="af638-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="af638-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="af638-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="af638-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="af638-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="af638-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="af638-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span><span class="sxs-lookup"><span data-stu-id="af638-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="af638-109">Supported versions</span><span class="sxs-lookup"><span data-stu-id="af638-109">Supported versions</span></span>
<span data-ttu-id="af638-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span><span class="sxs-lookup"><span data-stu-id="af638-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af638-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="af638-111">Prerequisites</span></span>
<span data-ttu-id="af638-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span><span class="sxs-lookup"><span data-stu-id="af638-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="af638-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span><span class="sxs-lookup"><span data-stu-id="af638-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="af638-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="af638-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="af638-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span><span class="sxs-lookup"><span data-stu-id="af638-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="af638-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="af638-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="af638-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="af638-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="af638-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="af638-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="af638-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="af638-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="af638-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="af638-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="af638-121">Getting started</span><span class="sxs-lookup"><span data-stu-id="af638-121">Getting started</span></span>
<span data-ttu-id="af638-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="af638-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="af638-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="af638-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="af638-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="af638-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="af638-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="af638-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="af638-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="af638-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="af638-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="af638-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="af638-128">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="af638-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="af638-129">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="af638-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="af638-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="af638-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="af638-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="af638-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="af638-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="af638-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="af638-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="af638-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="af638-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span><span class="sxs-lookup"><span data-stu-id="af638-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="af638-135">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="af638-135">Linked service properties</span></span>
<span data-ttu-id="af638-136">The following table provides description for JSON elements specific to Cassandra linked service.</span><span class="sxs-lookup"><span data-stu-id="af638-136">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="af638-137">Property</span><span class="sxs-lookup"><span data-stu-id="af638-137">Property</span></span> | <span data-ttu-id="af638-138">Description</span><span class="sxs-lookup"><span data-stu-id="af638-138">Description</span></span> | <span data-ttu-id="af638-139">Required</span><span class="sxs-lookup"><span data-stu-id="af638-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af638-140">type</span><span class="sxs-lookup"><span data-stu-id="af638-140">type</span></span> |<span data-ttu-id="af638-141">The type property must be set to: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="af638-141">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="af638-142">Yes</span><span class="sxs-lookup"><span data-stu-id="af638-142">Yes</span></span> |
| <span data-ttu-id="af638-143">host</span><span class="sxs-lookup"><span data-stu-id="af638-143">host</span></span> |<span data-ttu-id="af638-144">One or more IP addresses or host names of Cassandra servers.</span><span class="sxs-lookup"><span data-stu-id="af638-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="af638-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span><span class="sxs-lookup"><span data-stu-id="af638-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="af638-146">Yes</span><span class="sxs-lookup"><span data-stu-id="af638-146">Yes</span></span> |
| <span data-ttu-id="af638-147">port</span><span class="sxs-lookup"><span data-stu-id="af638-147">port</span></span> |<span data-ttu-id="af638-148">The TCP port that the Cassandra server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="af638-148">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="af638-149">No, default value: 9042</span><span class="sxs-lookup"><span data-stu-id="af638-149">No, default value: 9042</span></span> |
| <span data-ttu-id="af638-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="af638-150">authenticationType</span></span> |<span data-ttu-id="af638-151">Basic, or Anonymous</span><span class="sxs-lookup"><span data-stu-id="af638-151">Basic, or Anonymous</span></span> |<span data-ttu-id="af638-152">Yes</span><span class="sxs-lookup"><span data-stu-id="af638-152">Yes</span></span> |
| <span data-ttu-id="af638-153">username</span><span class="sxs-lookup"><span data-stu-id="af638-153">username</span></span> |<span data-ttu-id="af638-154">Specify user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="af638-154">Specify user name for the user account.</span></span> |<span data-ttu-id="af638-155">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="af638-155">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="af638-156">password</span><span class="sxs-lookup"><span data-stu-id="af638-156">password</span></span> |<span data-ttu-id="af638-157">Specify password for the user account.</span><span class="sxs-lookup"><span data-stu-id="af638-157">Specify password for the user account.</span></span> |<span data-ttu-id="af638-158">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="af638-158">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="af638-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="af638-159">gatewayName</span></span> |<span data-ttu-id="af638-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="af638-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="af638-161">Yes</span><span class="sxs-lookup"><span data-stu-id="af638-161">Yes</span></span> |
| <span data-ttu-id="af638-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="af638-162">encryptedCredential</span></span> |<span data-ttu-id="af638-163">Credential encrypted by the gateway.</span><span class="sxs-lookup"><span data-stu-id="af638-163">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="af638-164">No</span><span class="sxs-lookup"><span data-stu-id="af638-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="af638-165">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="af638-165">Dataset properties</span></span>
<span data-ttu-id="af638-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="af638-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="af638-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="af638-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="af638-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="af638-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="af638-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span><span class="sxs-lookup"><span data-stu-id="af638-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="af638-170">Property</span><span class="sxs-lookup"><span data-stu-id="af638-170">Property</span></span> | <span data-ttu-id="af638-171">Description</span><span class="sxs-lookup"><span data-stu-id="af638-171">Description</span></span> | <span data-ttu-id="af638-172">Required</span><span class="sxs-lookup"><span data-stu-id="af638-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af638-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="af638-173">keyspace</span></span> |<span data-ttu-id="af638-174">Name of the keyspace or schema in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="af638-174">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="af638-175">Yes (If **query** for **CassandraSource** is not defined).</span><span class="sxs-lookup"><span data-stu-id="af638-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="af638-176">tableName</span><span class="sxs-lookup"><span data-stu-id="af638-176">tableName</span></span> |<span data-ttu-id="af638-177">Name of the table in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="af638-177">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="af638-178">Yes (If **query** for **CassandraSource** is not defined).</span><span class="sxs-lookup"><span data-stu-id="af638-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="af638-179">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="af638-179">Copy activity properties</span></span>
<span data-ttu-id="af638-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="af638-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="af638-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="af638-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="af638-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="af638-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="af638-183">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="af638-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="af638-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="af638-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="af638-185">Property</span><span class="sxs-lookup"><span data-stu-id="af638-185">Property</span></span> | <span data-ttu-id="af638-186">Description</span><span class="sxs-lookup"><span data-stu-id="af638-186">Description</span></span> | <span data-ttu-id="af638-187">Allowed values</span><span class="sxs-lookup"><span data-stu-id="af638-187">Allowed values</span></span> | <span data-ttu-id="af638-188">Required</span><span class="sxs-lookup"><span data-stu-id="af638-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="af638-189">query</span><span class="sxs-lookup"><span data-stu-id="af638-189">query</span></span> |<span data-ttu-id="af638-190">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="af638-190">Use the custom query to read data.</span></span> |<span data-ttu-id="af638-191">SQL-92 query or CQL query.</span><span class="sxs-lookup"><span data-stu-id="af638-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="af638-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="af638-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="af638-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span><span class="sxs-lookup"><span data-stu-id="af638-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="af638-194">No (if tableName and keyspace on dataset are defined).</span><span class="sxs-lookup"><span data-stu-id="af638-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="af638-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="af638-195">consistencyLevel</span></span> |<span data-ttu-id="af638-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span><span class="sxs-lookup"><span data-stu-id="af638-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="af638-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span><span class="sxs-lookup"><span data-stu-id="af638-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="af638-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="af638-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="af638-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span><span class="sxs-lookup"><span data-stu-id="af638-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="af638-200">No.</span><span class="sxs-lookup"><span data-stu-id="af638-200">No.</span></span> <span data-ttu-id="af638-201">Default value is ONE.</span><span class="sxs-lookup"><span data-stu-id="af638-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="af638-202">JSON example: Copy data from Cassandra to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="af638-202">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="af638-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="af638-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="af638-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="af638-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="af638-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="af638-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af638-206">This sample provides JSON snippets.</span><span class="sxs-lookup"><span data-stu-id="af638-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="af638-207">It does not include step-by-step instructions for creating the data factory.</span><span class="sxs-lookup"><span data-stu-id="af638-207">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="af638-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="af638-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="af638-209">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="af638-209">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="af638-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="af638-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="af638-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="af638-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="af638-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="af638-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="af638-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="af638-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="af638-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="af638-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="af638-215">**Cassandra linked service:**</span><span class="sxs-lookup"><span data-stu-id="af638-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="af638-216">This example uses the **Cassandra** linked service.</span><span class="sxs-lookup"><span data-stu-id="af638-216">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="af638-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="af638-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="af638-218">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="af638-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="af638-219">**Cassandra input dataset:**</span><span class="sxs-lookup"><span data-stu-id="af638-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

<span data-ttu-id="af638-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="af638-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="af638-221">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="af638-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="af638-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="af638-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="af638-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="af638-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="af638-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="af638-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="af638-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="af638-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="af638-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="af638-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="af638-227">Type mapping for Cassandra</span><span class="sxs-lookup"><span data-stu-id="af638-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="af638-228">Cassandra Type</span><span class="sxs-lookup"><span data-stu-id="af638-228">Cassandra Type</span></span> | <span data-ttu-id="af638-229">.Net Based Type</span><span class="sxs-lookup"><span data-stu-id="af638-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="af638-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="af638-230">ASCII</span></span> |<span data-ttu-id="af638-231">String</span><span class="sxs-lookup"><span data-stu-id="af638-231">String</span></span> |
| <span data-ttu-id="af638-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="af638-232">BIGINT</span></span> |<span data-ttu-id="af638-233">Int64</span><span class="sxs-lookup"><span data-stu-id="af638-233">Int64</span></span> |
| <span data-ttu-id="af638-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="af638-234">BLOB</span></span> |<span data-ttu-id="af638-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="af638-235">Byte[]</span></span> |
| <span data-ttu-id="af638-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="af638-236">BOOLEAN</span></span> |<span data-ttu-id="af638-237">Boolean</span><span class="sxs-lookup"><span data-stu-id="af638-237">Boolean</span></span> |
| <span data-ttu-id="af638-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="af638-238">DECIMAL</span></span> |<span data-ttu-id="af638-239">Decimal</span><span class="sxs-lookup"><span data-stu-id="af638-239">Decimal</span></span> |
| <span data-ttu-id="af638-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="af638-240">DOUBLE</span></span> |<span data-ttu-id="af638-241">Double</span><span class="sxs-lookup"><span data-stu-id="af638-241">Double</span></span> |
| <span data-ttu-id="af638-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="af638-242">FLOAT</span></span> |<span data-ttu-id="af638-243">Single</span><span class="sxs-lookup"><span data-stu-id="af638-243">Single</span></span> |
| <span data-ttu-id="af638-244">INET</span><span class="sxs-lookup"><span data-stu-id="af638-244">INET</span></span> |<span data-ttu-id="af638-245">String</span><span class="sxs-lookup"><span data-stu-id="af638-245">String</span></span> |
| <span data-ttu-id="af638-246">INT</span><span class="sxs-lookup"><span data-stu-id="af638-246">INT</span></span> |<span data-ttu-id="af638-247">Int32</span><span class="sxs-lookup"><span data-stu-id="af638-247">Int32</span></span> |
| <span data-ttu-id="af638-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="af638-248">TEXT</span></span> |<span data-ttu-id="af638-249">String</span><span class="sxs-lookup"><span data-stu-id="af638-249">String</span></span> |
| <span data-ttu-id="af638-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="af638-250">TIMESTAMP</span></span> |<span data-ttu-id="af638-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="af638-251">DateTime</span></span> |
| <span data-ttu-id="af638-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="af638-252">TIMEUUID</span></span> |<span data-ttu-id="af638-253">Guid</span><span class="sxs-lookup"><span data-stu-id="af638-253">Guid</span></span> |
| <span data-ttu-id="af638-254">UUID</span><span class="sxs-lookup"><span data-stu-id="af638-254">UUID</span></span> |<span data-ttu-id="af638-255">Guid</span><span class="sxs-lookup"><span data-stu-id="af638-255">Guid</span></span> |
| <span data-ttu-id="af638-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="af638-256">VARCHAR</span></span> |<span data-ttu-id="af638-257">String</span><span class="sxs-lookup"><span data-stu-id="af638-257">String</span></span> |
| <span data-ttu-id="af638-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="af638-258">VARINT</span></span> |<span data-ttu-id="af638-259">Decimal</span><span class="sxs-lookup"><span data-stu-id="af638-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="af638-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span><span class="sxs-lookup"><span data-stu-id="af638-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="af638-261">User-defined types are not supported.</span><span class="sxs-lookup"><span data-stu-id="af638-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="af638-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span><span class="sxs-lookup"><span data-stu-id="af638-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="af638-263">Work with collections using virtual table</span><span class="sxs-lookup"><span data-stu-id="af638-263">Work with collections using virtual table</span></span>
<span data-ttu-id="af638-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="af638-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="af638-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span><span class="sxs-lookup"><span data-stu-id="af638-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="af638-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span><span class="sxs-lookup"><span data-stu-id="af638-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="af638-267">A **base table**, which contains the same data as the real table except for the collection columns.</span><span class="sxs-lookup"><span data-stu-id="af638-267">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="af638-268">The base table uses the same name as the real table that it represents.</span><span class="sxs-lookup"><span data-stu-id="af638-268">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="af638-269">A **virtual table** for each collection column, which expands the nested data.</span><span class="sxs-lookup"><span data-stu-id="af638-269">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="af638-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span><span class="sxs-lookup"><span data-stu-id="af638-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="af638-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span><span class="sxs-lookup"><span data-stu-id="af638-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="af638-272">See Example section for details.</span><span class="sxs-lookup"><span data-stu-id="af638-272">See Example section for details.</span></span> <span data-ttu-id="af638-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span><span class="sxs-lookup"><span data-stu-id="af638-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="af638-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span><span class="sxs-lookup"><span data-stu-id="af638-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="af638-275">You can also construct a query in the Copy Wizard and validate to see the result.</span><span class="sxs-lookup"><span data-stu-id="af638-275">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="af638-276">Example</span><span class="sxs-lookup"><span data-stu-id="af638-276">Example</span></span>
<span data-ttu-id="af638-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span><span class="sxs-lookup"><span data-stu-id="af638-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="af638-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="af638-278">pk_int</span></span> | <span data-ttu-id="af638-279">Value</span><span class="sxs-lookup"><span data-stu-id="af638-279">Value</span></span> | <span data-ttu-id="af638-280">List</span><span class="sxs-lookup"><span data-stu-id="af638-280">List</span></span> | <span data-ttu-id="af638-281">Map</span><span class="sxs-lookup"><span data-stu-id="af638-281">Map</span></span> | <span data-ttu-id="af638-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="af638-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="af638-283">1</span><span class="sxs-lookup"><span data-stu-id="af638-283">1</span></span> |<span data-ttu-id="af638-284">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="af638-284">"sample value 1"</span></span> |<span data-ttu-id="af638-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="af638-285">["1", "2", "3"]</span></span> |<span data-ttu-id="af638-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="af638-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="af638-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="af638-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="af638-288">3</span><span class="sxs-lookup"><span data-stu-id="af638-288">3</span></span> |<span data-ttu-id="af638-289">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="af638-289">"sample value 3"</span></span> |<span data-ttu-id="af638-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="af638-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="af638-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="af638-291">{"S1": "t"}</span></span> |<span data-ttu-id="af638-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="af638-292">{"A", "E"}</span></span> |

<span data-ttu-id="af638-293">The driver would generate multiple virtual tables to represent this single table.</span><span class="sxs-lookup"><span data-stu-id="af638-293">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="af638-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span><span class="sxs-lookup"><span data-stu-id="af638-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="af638-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span><span class="sxs-lookup"><span data-stu-id="af638-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="af638-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span><span class="sxs-lookup"><span data-stu-id="af638-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="af638-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="af638-297">pk_int</span></span> | <span data-ttu-id="af638-298">Value</span><span class="sxs-lookup"><span data-stu-id="af638-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="af638-299">1</span><span class="sxs-lookup"><span data-stu-id="af638-299">1</span></span> |<span data-ttu-id="af638-300">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="af638-300">"sample value 1"</span></span> |
| <span data-ttu-id="af638-301">3</span><span class="sxs-lookup"><span data-stu-id="af638-301">3</span></span> |<span data-ttu-id="af638-302">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="af638-302">"sample value 3"</span></span> |

<span data-ttu-id="af638-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span><span class="sxs-lookup"><span data-stu-id="af638-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="af638-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span><span class="sxs-lookup"><span data-stu-id="af638-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="af638-305">The columns with names that end with “_value” contain the expanded data from the collection.</span><span class="sxs-lookup"><span data-stu-id="af638-305">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="af638-306">Table “ExampleTable_vt_List”:</span><span class="sxs-lookup"><span data-stu-id="af638-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="af638-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="af638-307">pk_int</span></span> | <span data-ttu-id="af638-308">List_index</span><span class="sxs-lookup"><span data-stu-id="af638-308">List_index</span></span> | <span data-ttu-id="af638-309">List_value</span><span class="sxs-lookup"><span data-stu-id="af638-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af638-310">1</span><span class="sxs-lookup"><span data-stu-id="af638-310">1</span></span> |<span data-ttu-id="af638-311">0</span><span class="sxs-lookup"><span data-stu-id="af638-311">0</span></span> |<span data-ttu-id="af638-312">1</span><span class="sxs-lookup"><span data-stu-id="af638-312">1</span></span> |
| <span data-ttu-id="af638-313">1</span><span class="sxs-lookup"><span data-stu-id="af638-313">1</span></span> |<span data-ttu-id="af638-314">1</span><span class="sxs-lookup"><span data-stu-id="af638-314">1</span></span> |<span data-ttu-id="af638-315">2</span><span class="sxs-lookup"><span data-stu-id="af638-315">2</span></span> |
| <span data-ttu-id="af638-316">1</span><span class="sxs-lookup"><span data-stu-id="af638-316">1</span></span> |<span data-ttu-id="af638-317">2</span><span class="sxs-lookup"><span data-stu-id="af638-317">2</span></span> |<span data-ttu-id="af638-318">3</span><span class="sxs-lookup"><span data-stu-id="af638-318">3</span></span> |
| <span data-ttu-id="af638-319">3</span><span class="sxs-lookup"><span data-stu-id="af638-319">3</span></span> |<span data-ttu-id="af638-320">0</span><span class="sxs-lookup"><span data-stu-id="af638-320">0</span></span> |<span data-ttu-id="af638-321">100</span><span class="sxs-lookup"><span data-stu-id="af638-321">100</span></span> |
| <span data-ttu-id="af638-322">3</span><span class="sxs-lookup"><span data-stu-id="af638-322">3</span></span> |<span data-ttu-id="af638-323">1</span><span class="sxs-lookup"><span data-stu-id="af638-323">1</span></span> |<span data-ttu-id="af638-324">101</span><span class="sxs-lookup"><span data-stu-id="af638-324">101</span></span> |
| <span data-ttu-id="af638-325">3</span><span class="sxs-lookup"><span data-stu-id="af638-325">3</span></span> |<span data-ttu-id="af638-326">2</span><span class="sxs-lookup"><span data-stu-id="af638-326">2</span></span> |<span data-ttu-id="af638-327">102</span><span class="sxs-lookup"><span data-stu-id="af638-327">102</span></span> |
| <span data-ttu-id="af638-328">3</span><span class="sxs-lookup"><span data-stu-id="af638-328">3</span></span> |<span data-ttu-id="af638-329">3</span><span class="sxs-lookup"><span data-stu-id="af638-329">3</span></span> |<span data-ttu-id="af638-330">103</span><span class="sxs-lookup"><span data-stu-id="af638-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="af638-331">Table “ExampleTable_vt_Map”:</span><span class="sxs-lookup"><span data-stu-id="af638-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="af638-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="af638-332">pk_int</span></span> | <span data-ttu-id="af638-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="af638-333">Map_key</span></span> | <span data-ttu-id="af638-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="af638-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af638-335">1</span><span class="sxs-lookup"><span data-stu-id="af638-335">1</span></span> |<span data-ttu-id="af638-336">S1</span><span class="sxs-lookup"><span data-stu-id="af638-336">S1</span></span> |<span data-ttu-id="af638-337">A</span><span class="sxs-lookup"><span data-stu-id="af638-337">A</span></span> |
| <span data-ttu-id="af638-338">1</span><span class="sxs-lookup"><span data-stu-id="af638-338">1</span></span> |<span data-ttu-id="af638-339">S2</span><span class="sxs-lookup"><span data-stu-id="af638-339">S2</span></span> |<span data-ttu-id="af638-340">b</span><span class="sxs-lookup"><span data-stu-id="af638-340">b</span></span> |
| <span data-ttu-id="af638-341">3</span><span class="sxs-lookup"><span data-stu-id="af638-341">3</span></span> |<span data-ttu-id="af638-342">S1</span><span class="sxs-lookup"><span data-stu-id="af638-342">S1</span></span> |<span data-ttu-id="af638-343">t</span><span class="sxs-lookup"><span data-stu-id="af638-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="af638-344">Table “ExampleTable_vt_StringSet”:</span><span class="sxs-lookup"><span data-stu-id="af638-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="af638-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="af638-345">pk_int</span></span> | <span data-ttu-id="af638-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="af638-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="af638-347">1</span><span class="sxs-lookup"><span data-stu-id="af638-347">1</span></span> |<span data-ttu-id="af638-348">A</span><span class="sxs-lookup"><span data-stu-id="af638-348">A</span></span> |
| <span data-ttu-id="af638-349">1</span><span class="sxs-lookup"><span data-stu-id="af638-349">1</span></span> |<span data-ttu-id="af638-350">B</span><span class="sxs-lookup"><span data-stu-id="af638-350">B</span></span> |
| <span data-ttu-id="af638-351">1</span><span class="sxs-lookup"><span data-stu-id="af638-351">1</span></span> |<span data-ttu-id="af638-352">C</span><span class="sxs-lookup"><span data-stu-id="af638-352">C</span></span> |
| <span data-ttu-id="af638-353">3</span><span class="sxs-lookup"><span data-stu-id="af638-353">3</span></span> |<span data-ttu-id="af638-354">A</span><span class="sxs-lookup"><span data-stu-id="af638-354">A</span></span> |
| <span data-ttu-id="af638-355">3</span><span class="sxs-lookup"><span data-stu-id="af638-355">3</span></span> |<span data-ttu-id="af638-356">E</span><span class="sxs-lookup"><span data-stu-id="af638-356">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="af638-357">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="af638-357">Map source to sink columns</span></span>
<span data-ttu-id="af638-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="af638-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="af638-359">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="af638-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="af638-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="af638-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="af638-361">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="af638-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="af638-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="af638-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="af638-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="af638-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="af638-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="af638-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="af638-365">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="af638-365">Performance and Tuning</span></span>
<span data-ttu-id="af638-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="af638-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
