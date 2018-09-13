---
title: Move data from Cassandra using Data Factory | Microsoft Docs
description: Learn about how to move data from an on-premises Cassandra database using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/07/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: c4ed3a22d3ad4e227178e8ac265cc97050e31ee6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868070"
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="351fb-103">Move data from an on-premises Cassandra database using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="351fb-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-onprem-cassandra-connector.md)
> * [Version 2 (current version)](../connector-cassandra.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Cassandra connector in V2](../connector-cassandra.md).

<span data-ttu-id="351fb-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="351fb-108">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="351fb-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="351fb-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="351fb-110">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="351fb-110">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="351fb-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="351fb-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="351fb-112">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span><span class="sxs-lookup"><span data-stu-id="351fb-112">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="351fb-113">Supported versions</span><span class="sxs-lookup"><span data-stu-id="351fb-113">Supported versions</span></span>
<span data-ttu-id="351fb-114">The Cassandra connector supports the following versions of Cassandra: 2.x and 3.x.</span><span class="sxs-lookup"><span data-stu-id="351fb-114">The Cassandra connector supports the following versions of Cassandra: 2.x and 3.x.</span></span> <span data-ttu-id="351fb-115">For activity running on Self-hosted Integration Runtime, Cassandra 3.x is supported since IR version 3.7 and above.</span><span class="sxs-lookup"><span data-stu-id="351fb-115">For activity running on Self-hosted Integration Runtime, Cassandra 3.x is supported since IR version 3.7 and above.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="351fb-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="351fb-116">Prerequisites</span></span>
<span data-ttu-id="351fb-117">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span><span class="sxs-lookup"><span data-stu-id="351fb-117">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="351fb-118">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span><span class="sxs-lookup"><span data-stu-id="351fb-118">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="351fb-119">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="351fb-119">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="351fb-120">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span><span class="sxs-lookup"><span data-stu-id="351fb-120">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="351fb-121">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="351fb-121">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="351fb-122">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="351fb-122">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="351fb-123">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="351fb-123">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="351fb-124">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="351fb-124">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.

## <a name="getting-started"></a><span data-ttu-id="351fb-126">Getting started</span><span class="sxs-lookup"><span data-stu-id="351fb-126">Getting started</span></span>
<span data-ttu-id="351fb-127">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="351fb-127">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="351fb-128">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="351fb-128">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="351fb-129">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="351fb-129">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="351fb-130">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="351fb-130">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="351fb-131">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="351fb-131">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="351fb-132">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="351fb-132">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="351fb-133">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="351fb-133">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="351fb-134">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="351fb-134">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="351fb-135">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="351fb-135">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="351fb-136">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="351fb-136">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="351fb-137">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="351fb-137">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="351fb-138">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="351fb-138">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="351fb-139">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span><span class="sxs-lookup"><span data-stu-id="351fb-139">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="351fb-140">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="351fb-140">Linked service properties</span></span>
<span data-ttu-id="351fb-141">The following table provides description for JSON elements specific to Cassandra linked service.</span><span class="sxs-lookup"><span data-stu-id="351fb-141">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="351fb-142">Property</span><span class="sxs-lookup"><span data-stu-id="351fb-142">Property</span></span> | <span data-ttu-id="351fb-143">Description</span><span class="sxs-lookup"><span data-stu-id="351fb-143">Description</span></span> | <span data-ttu-id="351fb-144">Required</span><span class="sxs-lookup"><span data-stu-id="351fb-144">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="351fb-145">type</span><span class="sxs-lookup"><span data-stu-id="351fb-145">type</span></span> |<span data-ttu-id="351fb-146">The type property must be set to: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="351fb-146">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="351fb-147">Yes</span><span class="sxs-lookup"><span data-stu-id="351fb-147">Yes</span></span> |
| <span data-ttu-id="351fb-148">host</span><span class="sxs-lookup"><span data-stu-id="351fb-148">host</span></span> |<span data-ttu-id="351fb-149">One or more IP addresses or host names of Cassandra servers.</span><span class="sxs-lookup"><span data-stu-id="351fb-149">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="351fb-150">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span><span class="sxs-lookup"><span data-stu-id="351fb-150">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="351fb-151">Yes</span><span class="sxs-lookup"><span data-stu-id="351fb-151">Yes</span></span> |
| <span data-ttu-id="351fb-152">port</span><span class="sxs-lookup"><span data-stu-id="351fb-152">port</span></span> |<span data-ttu-id="351fb-153">The TCP port that the Cassandra server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="351fb-153">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="351fb-154">No, default value: 9042</span><span class="sxs-lookup"><span data-stu-id="351fb-154">No, default value: 9042</span></span> |
| <span data-ttu-id="351fb-155">authenticationType</span><span class="sxs-lookup"><span data-stu-id="351fb-155">authenticationType</span></span> |<span data-ttu-id="351fb-156">Basic, or Anonymous</span><span class="sxs-lookup"><span data-stu-id="351fb-156">Basic, or Anonymous</span></span> |<span data-ttu-id="351fb-157">Yes</span><span class="sxs-lookup"><span data-stu-id="351fb-157">Yes</span></span> |
| <span data-ttu-id="351fb-158">username</span><span class="sxs-lookup"><span data-stu-id="351fb-158">username</span></span> |<span data-ttu-id="351fb-159">Specify user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="351fb-159">Specify user name for the user account.</span></span> |<span data-ttu-id="351fb-160">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="351fb-160">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="351fb-161">password</span><span class="sxs-lookup"><span data-stu-id="351fb-161">password</span></span> |<span data-ttu-id="351fb-162">Specify password for the user account.</span><span class="sxs-lookup"><span data-stu-id="351fb-162">Specify password for the user account.</span></span> |<span data-ttu-id="351fb-163">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="351fb-163">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="351fb-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="351fb-164">gatewayName</span></span> |<span data-ttu-id="351fb-165">The name of the gateway that is used to connect to the on-premises Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="351fb-165">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="351fb-166">Yes</span><span class="sxs-lookup"><span data-stu-id="351fb-166">Yes</span></span> |
| <span data-ttu-id="351fb-167">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="351fb-167">encryptedCredential</span></span> |<span data-ttu-id="351fb-168">Credential encrypted by the gateway.</span><span class="sxs-lookup"><span data-stu-id="351fb-168">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="351fb-169">No</span><span class="sxs-lookup"><span data-stu-id="351fb-169">No</span></span> |

>[!NOTE]
>Currently connection to Cassandra using SSL is not supported.

## <a name="dataset-properties"></a><span data-ttu-id="351fb-171">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="351fb-171">Dataset properties</span></span>
<span data-ttu-id="351fb-172">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="351fb-172">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="351fb-173">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="351fb-173">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="351fb-174">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="351fb-174">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="351fb-175">The typeProperties section for dataset of type **CassandraTable** has the following properties</span><span class="sxs-lookup"><span data-stu-id="351fb-175">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="351fb-176">Property</span><span class="sxs-lookup"><span data-stu-id="351fb-176">Property</span></span> | <span data-ttu-id="351fb-177">Description</span><span class="sxs-lookup"><span data-stu-id="351fb-177">Description</span></span> | <span data-ttu-id="351fb-178">Required</span><span class="sxs-lookup"><span data-stu-id="351fb-178">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="351fb-179">keyspace</span><span class="sxs-lookup"><span data-stu-id="351fb-179">keyspace</span></span> |<span data-ttu-id="351fb-180">Name of the keyspace or schema in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="351fb-180">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="351fb-181">Yes (If **query** for **CassandraSource** is not defined).</span><span class="sxs-lookup"><span data-stu-id="351fb-181">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="351fb-182">tableName</span><span class="sxs-lookup"><span data-stu-id="351fb-182">tableName</span></span> |<span data-ttu-id="351fb-183">Name of the table in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="351fb-183">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="351fb-184">Yes (If **query** for **CassandraSource** is not defined).</span><span class="sxs-lookup"><span data-stu-id="351fb-184">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="351fb-185">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="351fb-185">Copy activity properties</span></span>
<span data-ttu-id="351fb-186">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="351fb-186">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="351fb-187">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="351fb-187">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="351fb-188">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="351fb-188">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="351fb-189">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="351fb-189">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="351fb-190">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="351fb-190">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="351fb-191">Property</span><span class="sxs-lookup"><span data-stu-id="351fb-191">Property</span></span> | <span data-ttu-id="351fb-192">Description</span><span class="sxs-lookup"><span data-stu-id="351fb-192">Description</span></span> | <span data-ttu-id="351fb-193">Allowed values</span><span class="sxs-lookup"><span data-stu-id="351fb-193">Allowed values</span></span> | <span data-ttu-id="351fb-194">Required</span><span class="sxs-lookup"><span data-stu-id="351fb-194">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="351fb-195">query</span><span class="sxs-lookup"><span data-stu-id="351fb-195">query</span></span> |<span data-ttu-id="351fb-196">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="351fb-196">Use the custom query to read data.</span></span> |<span data-ttu-id="351fb-197">SQL-92 query or CQL query.</span><span class="sxs-lookup"><span data-stu-id="351fb-197">SQL-92 query or CQL query.</span></span> <span data-ttu-id="351fb-198">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="351fb-198">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="351fb-199">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span><span class="sxs-lookup"><span data-stu-id="351fb-199">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="351fb-200">No (if tableName and keyspace on dataset are defined).</span><span class="sxs-lookup"><span data-stu-id="351fb-200">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="351fb-201">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="351fb-201">consistencyLevel</span></span> |<span data-ttu-id="351fb-202">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span><span class="sxs-lookup"><span data-stu-id="351fb-202">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="351fb-203">Cassandra checks the specified number of replicas for data to satisfy the read request.</span><span class="sxs-lookup"><span data-stu-id="351fb-203">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="351fb-204">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="351fb-204">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="351fb-205">See [Configuring data consistency](https://docs.datastax.com/en/cassandra/2.1/cassandra/dml/dml_config_consistency_c.html) for details.</span><span class="sxs-lookup"><span data-stu-id="351fb-205">See [Configuring data consistency](https://docs.datastax.com/en/cassandra/2.1/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="351fb-206">No.</span><span class="sxs-lookup"><span data-stu-id="351fb-206">No.</span></span> <span data-ttu-id="351fb-207">Default value is ONE.</span><span class="sxs-lookup"><span data-stu-id="351fb-207">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="351fb-208">JSON example: Copy data from Cassandra to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="351fb-208">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="351fb-209">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="351fb-209">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="351fb-210">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="351fb-210">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="351fb-211">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="351fb-211">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> This sample provides JSON snippets. It does not include step-by-step instructions for creating the data factory. See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.

<span data-ttu-id="351fb-215">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="351fb-215">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="351fb-216">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="351fb-216">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="351fb-217">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="351fb-217">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="351fb-218">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="351fb-218">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="351fb-219">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="351fb-219">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="351fb-220">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="351fb-220">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="351fb-221">**Cassandra linked service:**</span><span class="sxs-lookup"><span data-stu-id="351fb-221">**Cassandra linked service:**</span></span>

<span data-ttu-id="351fb-222">This example uses the **Cassandra** linked service.</span><span class="sxs-lookup"><span data-stu-id="351fb-222">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="351fb-223">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span><span class="sxs-lookup"><span data-stu-id="351fb-223">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

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

<span data-ttu-id="351fb-224">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="351fb-224">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="351fb-225">**Cassandra input dataset:**</span><span class="sxs-lookup"><span data-stu-id="351fb-225">**Cassandra input dataset:**</span></span>

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

<span data-ttu-id="351fb-226">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="351fb-226">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="351fb-227">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="351fb-227">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="351fb-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="351fb-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="351fb-229">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="351fb-229">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="351fb-230">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="351fb-230">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="351fb-231">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="351fb-231">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="351fb-232">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="351fb-232">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="351fb-233">Type mapping for Cassandra</span><span class="sxs-lookup"><span data-stu-id="351fb-233">Type mapping for Cassandra</span></span>
| <span data-ttu-id="351fb-234">Cassandra Type</span><span class="sxs-lookup"><span data-stu-id="351fb-234">Cassandra Type</span></span> | <span data-ttu-id="351fb-235">.Net Based Type</span><span class="sxs-lookup"><span data-stu-id="351fb-235">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="351fb-236">ASCII</span><span class="sxs-lookup"><span data-stu-id="351fb-236">ASCII</span></span> |<span data-ttu-id="351fb-237">String</span><span class="sxs-lookup"><span data-stu-id="351fb-237">String</span></span> |
| <span data-ttu-id="351fb-238">BIGINT</span><span class="sxs-lookup"><span data-stu-id="351fb-238">BIGINT</span></span> |<span data-ttu-id="351fb-239">Int64</span><span class="sxs-lookup"><span data-stu-id="351fb-239">Int64</span></span> |
| <span data-ttu-id="351fb-240">BLOB</span><span class="sxs-lookup"><span data-stu-id="351fb-240">BLOB</span></span> |<span data-ttu-id="351fb-241">Byte[]</span><span class="sxs-lookup"><span data-stu-id="351fb-241">Byte[]</span></span> |
| <span data-ttu-id="351fb-242">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="351fb-242">BOOLEAN</span></span> |<span data-ttu-id="351fb-243">Boolean</span><span class="sxs-lookup"><span data-stu-id="351fb-243">Boolean</span></span> |
| <span data-ttu-id="351fb-244">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="351fb-244">DECIMAL</span></span> |<span data-ttu-id="351fb-245">Decimal</span><span class="sxs-lookup"><span data-stu-id="351fb-245">Decimal</span></span> |
| <span data-ttu-id="351fb-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="351fb-246">DOUBLE</span></span> |<span data-ttu-id="351fb-247">Double</span><span class="sxs-lookup"><span data-stu-id="351fb-247">Double</span></span> |
| <span data-ttu-id="351fb-248">FLOAT</span><span class="sxs-lookup"><span data-stu-id="351fb-248">FLOAT</span></span> |<span data-ttu-id="351fb-249">Single</span><span class="sxs-lookup"><span data-stu-id="351fb-249">Single</span></span> |
| <span data-ttu-id="351fb-250">INET</span><span class="sxs-lookup"><span data-stu-id="351fb-250">INET</span></span> |<span data-ttu-id="351fb-251">String</span><span class="sxs-lookup"><span data-stu-id="351fb-251">String</span></span> |
| <span data-ttu-id="351fb-252">INT</span><span class="sxs-lookup"><span data-stu-id="351fb-252">INT</span></span> |<span data-ttu-id="351fb-253">Int32</span><span class="sxs-lookup"><span data-stu-id="351fb-253">Int32</span></span> |
| <span data-ttu-id="351fb-254">TEXT</span><span class="sxs-lookup"><span data-stu-id="351fb-254">TEXT</span></span> |<span data-ttu-id="351fb-255">String</span><span class="sxs-lookup"><span data-stu-id="351fb-255">String</span></span> |
| <span data-ttu-id="351fb-256">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="351fb-256">TIMESTAMP</span></span> |<span data-ttu-id="351fb-257">DateTime</span><span class="sxs-lookup"><span data-stu-id="351fb-257">DateTime</span></span> |
| <span data-ttu-id="351fb-258">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="351fb-258">TIMEUUID</span></span> |<span data-ttu-id="351fb-259">Guid</span><span class="sxs-lookup"><span data-stu-id="351fb-259">Guid</span></span> |
| <span data-ttu-id="351fb-260">UUID</span><span class="sxs-lookup"><span data-stu-id="351fb-260">UUID</span></span> |<span data-ttu-id="351fb-261">Guid</span><span class="sxs-lookup"><span data-stu-id="351fb-261">Guid</span></span> |
| <span data-ttu-id="351fb-262">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="351fb-262">VARCHAR</span></span> |<span data-ttu-id="351fb-263">String</span><span class="sxs-lookup"><span data-stu-id="351fb-263">String</span></span> |
| <span data-ttu-id="351fb-264">VARINT</span><span class="sxs-lookup"><span data-stu-id="351fb-264">VARINT</span></span> |<span data-ttu-id="351fb-265">Decimal</span><span class="sxs-lookup"><span data-stu-id="351fb-265">Decimal</span></span> |

> [!NOTE]
> For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.
>
> User-defined types are not supported.
>
> The length of Binary Column and String Column lengths cannot be greater than 4000.
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="351fb-269">Work with collections using virtual table</span><span class="sxs-lookup"><span data-stu-id="351fb-269">Work with collections using virtual table</span></span>
<span data-ttu-id="351fb-270">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="351fb-270">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="351fb-271">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span><span class="sxs-lookup"><span data-stu-id="351fb-271">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="351fb-272">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span><span class="sxs-lookup"><span data-stu-id="351fb-272">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="351fb-273">A **base table**, which contains the same data as the real table except for the collection columns.</span><span class="sxs-lookup"><span data-stu-id="351fb-273">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="351fb-274">The base table uses the same name as the real table that it represents.</span><span class="sxs-lookup"><span data-stu-id="351fb-274">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="351fb-275">A **virtual table** for each collection column, which expands the nested data.</span><span class="sxs-lookup"><span data-stu-id="351fb-275">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="351fb-276">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span><span class="sxs-lookup"><span data-stu-id="351fb-276">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="351fb-277">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span><span class="sxs-lookup"><span data-stu-id="351fb-277">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="351fb-278">See Example section for details.</span><span class="sxs-lookup"><span data-stu-id="351fb-278">See Example section for details.</span></span> <span data-ttu-id="351fb-279">You can access the content of Cassandra collections by querying and joining the virtual tables.</span><span class="sxs-lookup"><span data-stu-id="351fb-279">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="351fb-280">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span><span class="sxs-lookup"><span data-stu-id="351fb-280">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="351fb-281">You can also construct a query in the Copy Wizard and validate to see the result.</span><span class="sxs-lookup"><span data-stu-id="351fb-281">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="351fb-282">Example</span><span class="sxs-lookup"><span data-stu-id="351fb-282">Example</span></span>
<span data-ttu-id="351fb-283">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span><span class="sxs-lookup"><span data-stu-id="351fb-283">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="351fb-284">pk_int</span><span class="sxs-lookup"><span data-stu-id="351fb-284">pk_int</span></span> | <span data-ttu-id="351fb-285">Value</span><span class="sxs-lookup"><span data-stu-id="351fb-285">Value</span></span> | <span data-ttu-id="351fb-286">List</span><span class="sxs-lookup"><span data-stu-id="351fb-286">List</span></span> | <span data-ttu-id="351fb-287">Map</span><span class="sxs-lookup"><span data-stu-id="351fb-287">Map</span></span> | <span data-ttu-id="351fb-288">StringSet</span><span class="sxs-lookup"><span data-stu-id="351fb-288">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="351fb-289">1</span><span class="sxs-lookup"><span data-stu-id="351fb-289">1</span></span> |<span data-ttu-id="351fb-290">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="351fb-290">"sample value 1"</span></span> |<span data-ttu-id="351fb-291">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="351fb-291">["1", "2", "3"]</span></span> |<span data-ttu-id="351fb-292">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="351fb-292">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="351fb-293">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="351fb-293">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="351fb-294">3</span><span class="sxs-lookup"><span data-stu-id="351fb-294">3</span></span> |<span data-ttu-id="351fb-295">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="351fb-295">"sample value 3"</span></span> |<span data-ttu-id="351fb-296">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="351fb-296">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="351fb-297">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="351fb-297">{"S1": "t"}</span></span> |<span data-ttu-id="351fb-298">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="351fb-298">{"A", "E"}</span></span> |

<span data-ttu-id="351fb-299">The driver would generate multiple virtual tables to represent this single table.</span><span class="sxs-lookup"><span data-stu-id="351fb-299">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="351fb-300">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span><span class="sxs-lookup"><span data-stu-id="351fb-300">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="351fb-301">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span><span class="sxs-lookup"><span data-stu-id="351fb-301">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="351fb-302">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span><span class="sxs-lookup"><span data-stu-id="351fb-302">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="351fb-303">pk_int</span><span class="sxs-lookup"><span data-stu-id="351fb-303">pk_int</span></span> | <span data-ttu-id="351fb-304">Value</span><span class="sxs-lookup"><span data-stu-id="351fb-304">Value</span></span> |
| --- | --- |
| <span data-ttu-id="351fb-305">1</span><span class="sxs-lookup"><span data-stu-id="351fb-305">1</span></span> |<span data-ttu-id="351fb-306">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="351fb-306">"sample value 1"</span></span> |
| <span data-ttu-id="351fb-307">3</span><span class="sxs-lookup"><span data-stu-id="351fb-307">3</span></span> |<span data-ttu-id="351fb-308">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="351fb-308">"sample value 3"</span></span> |

<span data-ttu-id="351fb-309">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span><span class="sxs-lookup"><span data-stu-id="351fb-309">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="351fb-310">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span><span class="sxs-lookup"><span data-stu-id="351fb-310">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="351fb-311">The columns with names that end with “_value” contain the expanded data from the collection.</span><span class="sxs-lookup"><span data-stu-id="351fb-311">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="351fb-312">Table “ExampleTable_vt_List”:</span><span class="sxs-lookup"><span data-stu-id="351fb-312">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="351fb-313">pk_int</span><span class="sxs-lookup"><span data-stu-id="351fb-313">pk_int</span></span> | <span data-ttu-id="351fb-314">List_index</span><span class="sxs-lookup"><span data-stu-id="351fb-314">List_index</span></span> | <span data-ttu-id="351fb-315">List_value</span><span class="sxs-lookup"><span data-stu-id="351fb-315">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="351fb-316">1</span><span class="sxs-lookup"><span data-stu-id="351fb-316">1</span></span> |<span data-ttu-id="351fb-317">0</span><span class="sxs-lookup"><span data-stu-id="351fb-317">0</span></span> |<span data-ttu-id="351fb-318">1</span><span class="sxs-lookup"><span data-stu-id="351fb-318">1</span></span> |
| <span data-ttu-id="351fb-319">1</span><span class="sxs-lookup"><span data-stu-id="351fb-319">1</span></span> |<span data-ttu-id="351fb-320">1</span><span class="sxs-lookup"><span data-stu-id="351fb-320">1</span></span> |<span data-ttu-id="351fb-321">2</span><span class="sxs-lookup"><span data-stu-id="351fb-321">2</span></span> |
| <span data-ttu-id="351fb-322">1</span><span class="sxs-lookup"><span data-stu-id="351fb-322">1</span></span> |<span data-ttu-id="351fb-323">2</span><span class="sxs-lookup"><span data-stu-id="351fb-323">2</span></span> |<span data-ttu-id="351fb-324">3</span><span class="sxs-lookup"><span data-stu-id="351fb-324">3</span></span> |
| <span data-ttu-id="351fb-325">3</span><span class="sxs-lookup"><span data-stu-id="351fb-325">3</span></span> |<span data-ttu-id="351fb-326">0</span><span class="sxs-lookup"><span data-stu-id="351fb-326">0</span></span> |<span data-ttu-id="351fb-327">100</span><span class="sxs-lookup"><span data-stu-id="351fb-327">100</span></span> |
| <span data-ttu-id="351fb-328">3</span><span class="sxs-lookup"><span data-stu-id="351fb-328">3</span></span> |<span data-ttu-id="351fb-329">1</span><span class="sxs-lookup"><span data-stu-id="351fb-329">1</span></span> |<span data-ttu-id="351fb-330">101</span><span class="sxs-lookup"><span data-stu-id="351fb-330">101</span></span> |
| <span data-ttu-id="351fb-331">3</span><span class="sxs-lookup"><span data-stu-id="351fb-331">3</span></span> |<span data-ttu-id="351fb-332">2</span><span class="sxs-lookup"><span data-stu-id="351fb-332">2</span></span> |<span data-ttu-id="351fb-333">102</span><span class="sxs-lookup"><span data-stu-id="351fb-333">102</span></span> |
| <span data-ttu-id="351fb-334">3</span><span class="sxs-lookup"><span data-stu-id="351fb-334">3</span></span> |<span data-ttu-id="351fb-335">3</span><span class="sxs-lookup"><span data-stu-id="351fb-335">3</span></span> |<span data-ttu-id="351fb-336">103</span><span class="sxs-lookup"><span data-stu-id="351fb-336">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="351fb-337">Table “ExampleTable_vt_Map”:</span><span class="sxs-lookup"><span data-stu-id="351fb-337">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="351fb-338">pk_int</span><span class="sxs-lookup"><span data-stu-id="351fb-338">pk_int</span></span> | <span data-ttu-id="351fb-339">Map_key</span><span class="sxs-lookup"><span data-stu-id="351fb-339">Map_key</span></span> | <span data-ttu-id="351fb-340">Map_value</span><span class="sxs-lookup"><span data-stu-id="351fb-340">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="351fb-341">1</span><span class="sxs-lookup"><span data-stu-id="351fb-341">1</span></span> |<span data-ttu-id="351fb-342">S1</span><span class="sxs-lookup"><span data-stu-id="351fb-342">S1</span></span> |<span data-ttu-id="351fb-343">A</span><span class="sxs-lookup"><span data-stu-id="351fb-343">A</span></span> |
| <span data-ttu-id="351fb-344">1</span><span class="sxs-lookup"><span data-stu-id="351fb-344">1</span></span> |<span data-ttu-id="351fb-345">S2</span><span class="sxs-lookup"><span data-stu-id="351fb-345">S2</span></span> |<span data-ttu-id="351fb-346">b</span><span class="sxs-lookup"><span data-stu-id="351fb-346">b</span></span> |
| <span data-ttu-id="351fb-347">3</span><span class="sxs-lookup"><span data-stu-id="351fb-347">3</span></span> |<span data-ttu-id="351fb-348">S1</span><span class="sxs-lookup"><span data-stu-id="351fb-348">S1</span></span> |<span data-ttu-id="351fb-349">t</span><span class="sxs-lookup"><span data-stu-id="351fb-349">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="351fb-350">Table “ExampleTable_vt_StringSet”:</span><span class="sxs-lookup"><span data-stu-id="351fb-350">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="351fb-351">pk_int</span><span class="sxs-lookup"><span data-stu-id="351fb-351">pk_int</span></span> | <span data-ttu-id="351fb-352">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="351fb-352">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="351fb-353">1</span><span class="sxs-lookup"><span data-stu-id="351fb-353">1</span></span> |<span data-ttu-id="351fb-354">A</span><span class="sxs-lookup"><span data-stu-id="351fb-354">A</span></span> |
| <span data-ttu-id="351fb-355">1</span><span class="sxs-lookup"><span data-stu-id="351fb-355">1</span></span> |<span data-ttu-id="351fb-356">B</span><span class="sxs-lookup"><span data-stu-id="351fb-356">B</span></span> |
| <span data-ttu-id="351fb-357">1</span><span class="sxs-lookup"><span data-stu-id="351fb-357">1</span></span> |<span data-ttu-id="351fb-358">C</span><span class="sxs-lookup"><span data-stu-id="351fb-358">C</span></span> |
| <span data-ttu-id="351fb-359">3</span><span class="sxs-lookup"><span data-stu-id="351fb-359">3</span></span> |<span data-ttu-id="351fb-360">A</span><span class="sxs-lookup"><span data-stu-id="351fb-360">A</span></span> |
| <span data-ttu-id="351fb-361">3</span><span class="sxs-lookup"><span data-stu-id="351fb-361">3</span></span> |<span data-ttu-id="351fb-362">E</span><span class="sxs-lookup"><span data-stu-id="351fb-362">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="351fb-363">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="351fb-363">Map source to sink columns</span></span>
<span data-ttu-id="351fb-364">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="351fb-364">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="351fb-365">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="351fb-365">Repeatable read from relational sources</span></span>
<span data-ttu-id="351fb-366">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="351fb-366">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="351fb-367">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="351fb-367">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="351fb-368">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="351fb-368">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="351fb-369">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="351fb-369">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="351fb-370">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="351fb-370">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="351fb-371">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="351fb-371">Performance and Tuning</span></span>
<span data-ttu-id="351fb-372">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="351fb-372">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
