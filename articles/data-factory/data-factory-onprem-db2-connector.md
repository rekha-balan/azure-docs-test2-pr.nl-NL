---
title: Move data from DB2 using Azure Data Factory | Microsoft Docs
description: Learn about how move data from DB2 Database using Azure Data Factory
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: jingwang
ms.openlocfilehash: 6d54203797ad970d590b853b171b383708dbcb5d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564356"
---
# <a name="move-data-from-db2-using-azure-data-factory"></a><span data-ttu-id="24df7-103">Move data from DB2 using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="24df7-103">Move data from DB2 using Azure Data Factory</span></span>
<span data-ttu-id="24df7-104">This article outlines how you can use the Copy Activity in an Azure data factory to copy data from an on-premises DB2 database to any data store listed under Sink column in the [Supported Sources and Sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span><span class="sxs-lookup"><span data-stu-id="24df7-104">This article outlines how you can use the Copy Activity in an Azure data factory to copy data from an on-premises DB2 database to any data store listed under Sink column in the [Supported Sources and Sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span> <span data-ttu-id="24df7-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with copy activity and supported data store combinations.</span><span class="sxs-lookup"><span data-stu-id="24df7-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with copy activity and supported data store combinations.</span></span>

<span data-ttu-id="24df7-106">Data factory currently supports only moving data from a DB2 database to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but not moving data from other data stores to a DB2 database.</span><span class="sxs-lookup"><span data-stu-id="24df7-106">Data factory currently supports only moving data from a DB2 database to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but not moving data from other data stores to a DB2 database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24df7-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="24df7-107">Prerequisites</span></span>
<span data-ttu-id="24df7-108">Data Factory supports connecting to on-premises DB2 database using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="24df7-108">Data Factory supports connecting to on-premises DB2 database using the Data Management Gateway.</span></span> <span data-ttu-id="24df7-109">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span><span class="sxs-lookup"><span data-stu-id="24df7-109">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="24df7-110">Gateway is required even if the DB2 is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="24df7-110">Gateway is required even if the DB2 is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="24df7-111">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="24df7-111">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

<span data-ttu-id="24df7-112">The Data Management Gateway provides a built-in DB2 driver, therefore you don't need to manually install any driver when copying data from DB2.</span><span class="sxs-lookup"><span data-stu-id="24df7-112">The Data Management Gateway provides a built-in DB2 driver, therefore you don't need to manually install any driver when copying data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="24df7-113">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="24df7-113">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="24df7-114">Supported versions</span><span class="sxs-lookup"><span data-stu-id="24df7-114">Supported versions</span></span>
<span data-ttu-id="24df7-115">This DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager (SQLAM) version 9, 10 and 11:</span><span class="sxs-lookup"><span data-stu-id="24df7-115">This DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager (SQLAM) version 9, 10 and 11:</span></span>

* <span data-ttu-id="24df7-116">IBM DB2 for z/OS 11.1</span><span class="sxs-lookup"><span data-stu-id="24df7-116">IBM DB2 for z/OS 11.1</span></span>
* <span data-ttu-id="24df7-117">IBM DB2 for z/OS 10.1</span><span class="sxs-lookup"><span data-stu-id="24df7-117">IBM DB2 for z/OS 10.1</span></span>
* <span data-ttu-id="24df7-118">IBM DB2 for i 7.2</span><span class="sxs-lookup"><span data-stu-id="24df7-118">IBM DB2 for i 7.2</span></span>
* <span data-ttu-id="24df7-119">IBM DB2 for i 7.1</span><span class="sxs-lookup"><span data-stu-id="24df7-119">IBM DB2 for i 7.1</span></span>
* <span data-ttu-id="24df7-120">IBM DB2 for LUW 11</span><span class="sxs-lookup"><span data-stu-id="24df7-120">IBM DB2 for LUW 11</span></span>
* <span data-ttu-id="24df7-121">IBM DB2 for LUW 10.5</span><span class="sxs-lookup"><span data-stu-id="24df7-121">IBM DB2 for LUW 10.5</span></span>
* <span data-ttu-id="24df7-122">IBM DB2 for LUW 10.1</span><span class="sxs-lookup"><span data-stu-id="24df7-122">IBM DB2 for LUW 10.1</span></span>

> [!TIP]
> <span data-ttu-id="24df7-123">If you hit error stating "The package corresponding to an SQL statement execution request was not found.</span><span class="sxs-lookup"><span data-stu-id="24df7-123">If you hit error stating "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="24df7-124">SQLSTATE=51002 SQLCODE=-805", user a high privilege account (power user or admin) to run the copy activity once, then the needed package will be auto created during copy.</span><span class="sxs-lookup"><span data-stu-id="24df7-124">SQLSTATE=51002 SQLCODE=-805", user a high privilege account (power user or admin) to run the copy activity once, then the needed package will be auto created during copy.</span></span> <span data-ttu-id="24df7-125">Afterwards, you can switch back to normal user for your subsequent copy runs.</span><span class="sxs-lookup"><span data-stu-id="24df7-125">Afterwards, you can switch back to normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="24df7-126">Getting started</span><span class="sxs-lookup"><span data-stu-id="24df7-126">Getting started</span></span>
<span data-ttu-id="24df7-127">You can create a pipeline with a copy activity that moves data from an on-premises DB2 data store by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="24df7-127">You can create a pipeline with a copy activity that moves data from an on-premises DB2 data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="24df7-128">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="24df7-128">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="24df7-129">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="24df7-129">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="24df7-130">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="24df7-130">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="24df7-131">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="24df7-131">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="24df7-132">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="24df7-132">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="24df7-133">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="24df7-133">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="24df7-134">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="24df7-134">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="24df7-135">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="24df7-135">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="24df7-136">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="24df7-136">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="24df7-137">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="24df7-137">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="24df7-138">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises DB2 data store, see [JSON example: Copy data from DB2 to Azure Blob](#json-example-copy-data-from-db2-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="24df7-138">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises DB2 data store, see [JSON example: Copy data from DB2 to Azure Blob](#json-example-copy-data-from-db2-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="24df7-139">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a DB2 data store:</span><span class="sxs-lookup"><span data-stu-id="24df7-139">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a DB2 data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="24df7-140">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="24df7-140">Linked service properties</span></span>
<span data-ttu-id="24df7-141">The following table provides description for JSON elements specific to DB2 linked service.</span><span class="sxs-lookup"><span data-stu-id="24df7-141">The following table provides description for JSON elements specific to DB2 linked service.</span></span>

| <span data-ttu-id="24df7-142">Property</span><span class="sxs-lookup"><span data-stu-id="24df7-142">Property</span></span> | <span data-ttu-id="24df7-143">Description</span><span class="sxs-lookup"><span data-stu-id="24df7-143">Description</span></span> | <span data-ttu-id="24df7-144">Required</span><span class="sxs-lookup"><span data-stu-id="24df7-144">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24df7-145">type</span><span class="sxs-lookup"><span data-stu-id="24df7-145">type</span></span> |<span data-ttu-id="24df7-146">The type property must be set to: **OnPremisesDB2**</span><span class="sxs-lookup"><span data-stu-id="24df7-146">The type property must be set to: **OnPremisesDB2**</span></span> |<span data-ttu-id="24df7-147">Yes</span><span class="sxs-lookup"><span data-stu-id="24df7-147">Yes</span></span> |
| <span data-ttu-id="24df7-148">server</span><span class="sxs-lookup"><span data-stu-id="24df7-148">server</span></span> |<span data-ttu-id="24df7-149">Name of the DB2 server.</span><span class="sxs-lookup"><span data-stu-id="24df7-149">Name of the DB2 server.</span></span> |<span data-ttu-id="24df7-150">Yes</span><span class="sxs-lookup"><span data-stu-id="24df7-150">Yes</span></span> |
| <span data-ttu-id="24df7-151">database</span><span class="sxs-lookup"><span data-stu-id="24df7-151">database</span></span> |<span data-ttu-id="24df7-152">Name of the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="24df7-152">Name of the DB2 database.</span></span> |<span data-ttu-id="24df7-153">Yes</span><span class="sxs-lookup"><span data-stu-id="24df7-153">Yes</span></span> |
| <span data-ttu-id="24df7-154">schema</span><span class="sxs-lookup"><span data-stu-id="24df7-154">schema</span></span> |<span data-ttu-id="24df7-155">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="24df7-155">Name of the schema in the database.</span></span> <span data-ttu-id="24df7-156">The schema name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="24df7-156">The schema name is case-sensitive.</span></span> |<span data-ttu-id="24df7-157">No</span><span class="sxs-lookup"><span data-stu-id="24df7-157">No</span></span> |
| <span data-ttu-id="24df7-158">authenticationType</span><span class="sxs-lookup"><span data-stu-id="24df7-158">authenticationType</span></span> |<span data-ttu-id="24df7-159">Type of authentication used to connect to the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="24df7-159">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="24df7-160">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="24df7-160">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="24df7-161">Yes</span><span class="sxs-lookup"><span data-stu-id="24df7-161">Yes</span></span> |
| <span data-ttu-id="24df7-162">username</span><span class="sxs-lookup"><span data-stu-id="24df7-162">username</span></span> |<span data-ttu-id="24df7-163">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="24df7-163">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="24df7-164">No</span><span class="sxs-lookup"><span data-stu-id="24df7-164">No</span></span> |
| <span data-ttu-id="24df7-165">password</span><span class="sxs-lookup"><span data-stu-id="24df7-165">password</span></span> |<span data-ttu-id="24df7-166">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="24df7-166">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="24df7-167">No</span><span class="sxs-lookup"><span data-stu-id="24df7-167">No</span></span> |
| <span data-ttu-id="24df7-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="24df7-168">gatewayName</span></span> |<span data-ttu-id="24df7-169">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span><span class="sxs-lookup"><span data-stu-id="24df7-169">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="24df7-170">Yes</span><span class="sxs-lookup"><span data-stu-id="24df7-170">Yes</span></span> |


## <a name="dataset-properties"></a><span data-ttu-id="24df7-171">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="24df7-171">Dataset properties</span></span>
<span data-ttu-id="24df7-172">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="24df7-172">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="24df7-173">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="24df7-173">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="24df7-174">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="24df7-174">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="24df7-175">The typeProperties section for dataset of type RelationalTable (which includes DB2 dataset) has the following properties.</span><span class="sxs-lookup"><span data-stu-id="24df7-175">The typeProperties section for dataset of type RelationalTable (which includes DB2 dataset) has the following properties.</span></span>

| <span data-ttu-id="24df7-176">Property</span><span class="sxs-lookup"><span data-stu-id="24df7-176">Property</span></span> | <span data-ttu-id="24df7-177">Description</span><span class="sxs-lookup"><span data-stu-id="24df7-177">Description</span></span> | <span data-ttu-id="24df7-178">Required</span><span class="sxs-lookup"><span data-stu-id="24df7-178">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24df7-179">tableName</span><span class="sxs-lookup"><span data-stu-id="24df7-179">tableName</span></span> |<span data-ttu-id="24df7-180">Name of the table in the DB2 Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="24df7-180">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="24df7-181">The tableName is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="24df7-181">The tableName is case-sensitive.</span></span> |<span data-ttu-id="24df7-182">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="24df7-182">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="24df7-183">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="24df7-183">Copy activity properties</span></span>
<span data-ttu-id="24df7-184">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="24df7-184">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="24df7-185">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="24df7-185">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="24df7-186">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="24df7-186">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="24df7-187">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="24df7-187">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="24df7-188">For Copy Activity, when source is of type **RelationalSource** (which includes DB2) the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="24df7-188">For Copy Activity, when source is of type **RelationalSource** (which includes DB2) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="24df7-189">Property</span><span class="sxs-lookup"><span data-stu-id="24df7-189">Property</span></span> | <span data-ttu-id="24df7-190">Description</span><span class="sxs-lookup"><span data-stu-id="24df7-190">Description</span></span> | <span data-ttu-id="24df7-191">Allowed values</span><span class="sxs-lookup"><span data-stu-id="24df7-191">Allowed values</span></span> | <span data-ttu-id="24df7-192">Required</span><span class="sxs-lookup"><span data-stu-id="24df7-192">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="24df7-193">query</span><span class="sxs-lookup"><span data-stu-id="24df7-193">query</span></span> |<span data-ttu-id="24df7-194">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="24df7-194">Use the custom query to read data.</span></span> |<span data-ttu-id="24df7-195">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="24df7-195">SQL query string.</span></span> <span data-ttu-id="24df7-196">For example: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="24df7-196">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="24df7-197">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="24df7-197">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="24df7-198">Schema and table names are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="24df7-198">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="24df7-199">Enclose the names in "" (double quotes) in the query.</span><span class="sxs-lookup"><span data-stu-id="24df7-199">Enclose the names in "" (double quotes) in the query.</span></span>  

<span data-ttu-id="24df7-200">**Example:**</span><span class="sxs-lookup"><span data-stu-id="24df7-200">**Example:**</span></span>

```sql
"query": "select * from "DB2ADMIN"."Customers""
```


## <a name="json-example-copy-data-from-db2-to-azure-blob"></a><span data-ttu-id="24df7-201">JSON example: Copy data from DB2 to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="24df7-201">JSON example: Copy data from DB2 to Azure Blob</span></span>
<span data-ttu-id="24df7-202">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="24df7-202">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="24df7-203">It shows how to copy data from DB2 database and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="24df7-203">It shows how to copy data from DB2 database and Azure Blob Storage.</span></span> <span data-ttu-id="24df7-204">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="24df7-204">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="24df7-205">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="24df7-205">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="24df7-206">A linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="24df7-206">A linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="24df7-207">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="24df7-207">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="24df7-208">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="24df7-208">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="24df7-209">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="24df7-209">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="24df7-210">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="24df7-210">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="24df7-211">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span><span class="sxs-lookup"><span data-stu-id="24df7-211">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="24df7-212">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="24df7-212">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="24df7-213">As a first step, install and configure a data management gateway.</span><span class="sxs-lookup"><span data-stu-id="24df7-213">As a first step, install and configure a data management gateway.</span></span> <span data-ttu-id="24df7-214">Instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="24df7-214">Instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="24df7-215">**DB2 linked service:**</span><span class="sxs-lookup"><span data-stu-id="24df7-215">**DB2 linked service:**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

<span data-ttu-id="24df7-216">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="24df7-216">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="24df7-217">**DB2 input dataset:**</span><span class="sxs-lookup"><span data-stu-id="24df7-217">**DB2 input dataset:**</span></span>

<span data-ttu-id="24df7-218">The sample assumes you have created a table “MyTable” in DB2 and it contains a column called “timestamp” for time series data.</span><span class="sxs-lookup"><span data-stu-id="24df7-218">The sample assumes you have created a table “MyTable” in DB2 and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="24df7-219">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="24df7-219">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="24df7-220">Notice that the **type** is set to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="24df7-220">Notice that the **type** is set to **RelationalTable**.</span></span>

```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

<span data-ttu-id="24df7-221">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="24df7-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="24df7-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="24df7-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="24df7-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="24df7-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="24df7-224">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="24df7-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="24df7-225">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="24df7-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="24df7-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="24df7-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="24df7-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="24df7-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="24df7-228">The SQL query specified for the **query** property selects the data from the Orders table.</span><span class="sxs-lookup"><span data-stu-id="24df7-228">The SQL query specified for the **query** property selects the data from the Orders table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```


## <a name="type-mapping-for-db2"></a><span data-ttu-id="24df7-229">Type mapping for DB2</span><span class="sxs-lookup"><span data-stu-id="24df7-229">Type mapping for DB2</span></span>
<span data-ttu-id="24df7-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="24df7-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="24df7-231">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="24df7-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="24df7-232">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="24df7-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="24df7-233">When moving data to DB2, the following mappings are used from DB2 type to .NET type.</span><span class="sxs-lookup"><span data-stu-id="24df7-233">When moving data to DB2, the following mappings are used from DB2 type to .NET type.</span></span>

| <span data-ttu-id="24df7-234">DB2 Database type</span><span class="sxs-lookup"><span data-stu-id="24df7-234">DB2 Database type</span></span> | <span data-ttu-id="24df7-235">.NET Framework type</span><span class="sxs-lookup"><span data-stu-id="24df7-235">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="24df7-236">SmallInt</span><span class="sxs-lookup"><span data-stu-id="24df7-236">SmallInt</span></span> |<span data-ttu-id="24df7-237">Int16</span><span class="sxs-lookup"><span data-stu-id="24df7-237">Int16</span></span> |
| <span data-ttu-id="24df7-238">Integer</span><span class="sxs-lookup"><span data-stu-id="24df7-238">Integer</span></span> |<span data-ttu-id="24df7-239">Int32</span><span class="sxs-lookup"><span data-stu-id="24df7-239">Int32</span></span> |
| <span data-ttu-id="24df7-240">BigInt</span><span class="sxs-lookup"><span data-stu-id="24df7-240">BigInt</span></span> |<span data-ttu-id="24df7-241">Int64</span><span class="sxs-lookup"><span data-stu-id="24df7-241">Int64</span></span> |
| <span data-ttu-id="24df7-242">Real</span><span class="sxs-lookup"><span data-stu-id="24df7-242">Real</span></span> |<span data-ttu-id="24df7-243">Single</span><span class="sxs-lookup"><span data-stu-id="24df7-243">Single</span></span> |
| <span data-ttu-id="24df7-244">Double</span><span class="sxs-lookup"><span data-stu-id="24df7-244">Double</span></span> |<span data-ttu-id="24df7-245">Double</span><span class="sxs-lookup"><span data-stu-id="24df7-245">Double</span></span> |
| <span data-ttu-id="24df7-246">Float</span><span class="sxs-lookup"><span data-stu-id="24df7-246">Float</span></span> |<span data-ttu-id="24df7-247">Double</span><span class="sxs-lookup"><span data-stu-id="24df7-247">Double</span></span> |
| <span data-ttu-id="24df7-248">Decimal</span><span class="sxs-lookup"><span data-stu-id="24df7-248">Decimal</span></span> |<span data-ttu-id="24df7-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="24df7-249">Decimal</span></span> |
| <span data-ttu-id="24df7-250">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="24df7-250">DecimalFloat</span></span> |<span data-ttu-id="24df7-251">Decimal</span><span class="sxs-lookup"><span data-stu-id="24df7-251">Decimal</span></span> |
| <span data-ttu-id="24df7-252">Numeric</span><span class="sxs-lookup"><span data-stu-id="24df7-252">Numeric</span></span> |<span data-ttu-id="24df7-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="24df7-253">Decimal</span></span> |
| <span data-ttu-id="24df7-254">Date</span><span class="sxs-lookup"><span data-stu-id="24df7-254">Date</span></span> |<span data-ttu-id="24df7-255">Datetime</span><span class="sxs-lookup"><span data-stu-id="24df7-255">Datetime</span></span> |
| <span data-ttu-id="24df7-256">Time</span><span class="sxs-lookup"><span data-stu-id="24df7-256">Time</span></span> |<span data-ttu-id="24df7-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="24df7-257">TimeSpan</span></span> |
| <span data-ttu-id="24df7-258">Timestamp</span><span class="sxs-lookup"><span data-stu-id="24df7-258">Timestamp</span></span> |<span data-ttu-id="24df7-259">DateTime</span><span class="sxs-lookup"><span data-stu-id="24df7-259">DateTime</span></span> |
| <span data-ttu-id="24df7-260">Xml</span><span class="sxs-lookup"><span data-stu-id="24df7-260">Xml</span></span> |<span data-ttu-id="24df7-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="24df7-261">Byte[]</span></span> |
| <span data-ttu-id="24df7-262">Char</span><span class="sxs-lookup"><span data-stu-id="24df7-262">Char</span></span> |<span data-ttu-id="24df7-263">String</span><span class="sxs-lookup"><span data-stu-id="24df7-263">String</span></span> |
| <span data-ttu-id="24df7-264">VarChar</span><span class="sxs-lookup"><span data-stu-id="24df7-264">VarChar</span></span> |<span data-ttu-id="24df7-265">String</span><span class="sxs-lookup"><span data-stu-id="24df7-265">String</span></span> |
| <span data-ttu-id="24df7-266">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="24df7-266">LongVarChar</span></span> |<span data-ttu-id="24df7-267">String</span><span class="sxs-lookup"><span data-stu-id="24df7-267">String</span></span> |
| <span data-ttu-id="24df7-268">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="24df7-268">DB2DynArray</span></span> |<span data-ttu-id="24df7-269">String</span><span class="sxs-lookup"><span data-stu-id="24df7-269">String</span></span> |
| <span data-ttu-id="24df7-270">Binary</span><span class="sxs-lookup"><span data-stu-id="24df7-270">Binary</span></span> |<span data-ttu-id="24df7-271">Byte[]</span><span class="sxs-lookup"><span data-stu-id="24df7-271">Byte[]</span></span> |
| <span data-ttu-id="24df7-272">VarBinary</span><span class="sxs-lookup"><span data-stu-id="24df7-272">VarBinary</span></span> |<span data-ttu-id="24df7-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="24df7-273">Byte[]</span></span> |
| <span data-ttu-id="24df7-274">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="24df7-274">LongVarBinary</span></span> |<span data-ttu-id="24df7-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="24df7-275">Byte[]</span></span> |
| <span data-ttu-id="24df7-276">Graphic</span><span class="sxs-lookup"><span data-stu-id="24df7-276">Graphic</span></span> |<span data-ttu-id="24df7-277">String</span><span class="sxs-lookup"><span data-stu-id="24df7-277">String</span></span> |
| <span data-ttu-id="24df7-278">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="24df7-278">VarGraphic</span></span> |<span data-ttu-id="24df7-279">String</span><span class="sxs-lookup"><span data-stu-id="24df7-279">String</span></span> |
| <span data-ttu-id="24df7-280">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="24df7-280">LongVarGraphic</span></span> |<span data-ttu-id="24df7-281">String</span><span class="sxs-lookup"><span data-stu-id="24df7-281">String</span></span> |
| <span data-ttu-id="24df7-282">Clob</span><span class="sxs-lookup"><span data-stu-id="24df7-282">Clob</span></span> |<span data-ttu-id="24df7-283">String</span><span class="sxs-lookup"><span data-stu-id="24df7-283">String</span></span> |
| <span data-ttu-id="24df7-284">Blob</span><span class="sxs-lookup"><span data-stu-id="24df7-284">Blob</span></span> |<span data-ttu-id="24df7-285">Byte[]</span><span class="sxs-lookup"><span data-stu-id="24df7-285">Byte[]</span></span> |
| <span data-ttu-id="24df7-286">DbClob</span><span class="sxs-lookup"><span data-stu-id="24df7-286">DbClob</span></span> |<span data-ttu-id="24df7-287">String</span><span class="sxs-lookup"><span data-stu-id="24df7-287">String</span></span> |
| <span data-ttu-id="24df7-288">SmallInt</span><span class="sxs-lookup"><span data-stu-id="24df7-288">SmallInt</span></span> |<span data-ttu-id="24df7-289">Int16</span><span class="sxs-lookup"><span data-stu-id="24df7-289">Int16</span></span> |
| <span data-ttu-id="24df7-290">Integer</span><span class="sxs-lookup"><span data-stu-id="24df7-290">Integer</span></span> |<span data-ttu-id="24df7-291">Int32</span><span class="sxs-lookup"><span data-stu-id="24df7-291">Int32</span></span> |
| <span data-ttu-id="24df7-292">BigInt</span><span class="sxs-lookup"><span data-stu-id="24df7-292">BigInt</span></span> |<span data-ttu-id="24df7-293">Int64</span><span class="sxs-lookup"><span data-stu-id="24df7-293">Int64</span></span> |
| <span data-ttu-id="24df7-294">Real</span><span class="sxs-lookup"><span data-stu-id="24df7-294">Real</span></span> |<span data-ttu-id="24df7-295">Single</span><span class="sxs-lookup"><span data-stu-id="24df7-295">Single</span></span> |
| <span data-ttu-id="24df7-296">Double</span><span class="sxs-lookup"><span data-stu-id="24df7-296">Double</span></span> |<span data-ttu-id="24df7-297">Double</span><span class="sxs-lookup"><span data-stu-id="24df7-297">Double</span></span> |
| <span data-ttu-id="24df7-298">Float</span><span class="sxs-lookup"><span data-stu-id="24df7-298">Float</span></span> |<span data-ttu-id="24df7-299">Double</span><span class="sxs-lookup"><span data-stu-id="24df7-299">Double</span></span> |
| <span data-ttu-id="24df7-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="24df7-300">Decimal</span></span> |<span data-ttu-id="24df7-301">Decimal</span><span class="sxs-lookup"><span data-stu-id="24df7-301">Decimal</span></span> |
| <span data-ttu-id="24df7-302">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="24df7-302">DecimalFloat</span></span> |<span data-ttu-id="24df7-303">Decimal</span><span class="sxs-lookup"><span data-stu-id="24df7-303">Decimal</span></span> |
| <span data-ttu-id="24df7-304">Numeric</span><span class="sxs-lookup"><span data-stu-id="24df7-304">Numeric</span></span> |<span data-ttu-id="24df7-305">Decimal</span><span class="sxs-lookup"><span data-stu-id="24df7-305">Decimal</span></span> |
| <span data-ttu-id="24df7-306">Date</span><span class="sxs-lookup"><span data-stu-id="24df7-306">Date</span></span> |<span data-ttu-id="24df7-307">Datetime</span><span class="sxs-lookup"><span data-stu-id="24df7-307">Datetime</span></span> |
| <span data-ttu-id="24df7-308">Time</span><span class="sxs-lookup"><span data-stu-id="24df7-308">Time</span></span> |<span data-ttu-id="24df7-309">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="24df7-309">TimeSpan</span></span> |
| <span data-ttu-id="24df7-310">Timestamp</span><span class="sxs-lookup"><span data-stu-id="24df7-310">Timestamp</span></span> |<span data-ttu-id="24df7-311">DateTime</span><span class="sxs-lookup"><span data-stu-id="24df7-311">DateTime</span></span> |
| <span data-ttu-id="24df7-312">Xml</span><span class="sxs-lookup"><span data-stu-id="24df7-312">Xml</span></span> |<span data-ttu-id="24df7-313">Byte[]</span><span class="sxs-lookup"><span data-stu-id="24df7-313">Byte[]</span></span> |
| <span data-ttu-id="24df7-314">Char</span><span class="sxs-lookup"><span data-stu-id="24df7-314">Char</span></span> |<span data-ttu-id="24df7-315">String</span><span class="sxs-lookup"><span data-stu-id="24df7-315">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="24df7-316">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="24df7-316">Map source to sink columns</span></span>
<span data-ttu-id="24df7-317">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="24df7-317">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="24df7-318">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="24df7-318">Repeatable read from relational sources</span></span>
<span data-ttu-id="24df7-319">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="24df7-319">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="24df7-320">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="24df7-320">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="24df7-321">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="24df7-321">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="24df7-322">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="24df7-322">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="24df7-323">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="24df7-323">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="24df7-324">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="24df7-324">Performance and Tuning</span></span>
<span data-ttu-id="24df7-325">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="24df7-325">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
