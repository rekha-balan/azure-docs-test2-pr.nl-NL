---
title: Move data to/from Oracle using Data Factory | Microsoft Docs
description: Learn how to move data to/from Oracle database that is on-premises using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jingwang
ms.openlocfilehash: 750dfb2ff8b4d82b2f42518c3873a32d6be0bc20
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661607"
---
# <a name="move-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="969d1-103">Move data to/from on-premises Oracle using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="969d1-103">Move data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="969d1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span><span class="sxs-lookup"><span data-stu-id="969d1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="969d1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="969d1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="969d1-106">You can copy data from any supported source data store to Oracle database or from Oracle database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="969d1-106">You can copy data from any supported source data store to Oracle database or from Oracle database to any supported sink data store.</span></span> <span data-ttu-id="969d1-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="969d1-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="969d1-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="969d1-108">Prerequisites</span></span>
<span data-ttu-id="969d1-109">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="969d1-109">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="969d1-110">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span><span class="sxs-lookup"><span data-stu-id="969d1-110">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="969d1-111">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="969d1-111">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="969d1-112">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="969d1-112">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="969d1-113">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="969d1-113">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="969d1-114">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="969d1-114">Supported versions and installation</span></span>
<span data-ttu-id="969d1-115">This Oracle connector support two versions of drivers:</span><span class="sxs-lookup"><span data-stu-id="969d1-115">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="969d1-116">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span><span class="sxs-lookup"><span data-stu-id="969d1-116">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="969d1-117">Oracle Database version 10g Release 2 or later are supported.</span><span class="sxs-lookup"><span data-stu-id="969d1-117">Oracle Database version 10g Release 2 or later are supported.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="969d1-118">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span><span class="sxs-lookup"><span data-stu-id="969d1-118">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="969d1-119">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span><span class="sxs-lookup"><span data-stu-id="969d1-119">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="969d1-120">Alternatively, you can use the copy wizard to validate the connectivity.</span><span class="sxs-lookup"><span data-stu-id="969d1-120">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
    >

- <span data-ttu-id="969d1-121">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span><span class="sxs-lookup"><span data-stu-id="969d1-121">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="969d1-122">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="969d1-122">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="969d1-123">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span><span class="sxs-lookup"><span data-stu-id="969d1-123">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="969d1-124">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span><span class="sxs-lookup"><span data-stu-id="969d1-124">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="969d1-125">If you choose “XCopy Installation”, follow steps in the readme.htm.</span><span class="sxs-lookup"><span data-stu-id="969d1-125">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="969d1-126">We recommend you choose the installer with UI (non-XCopy one).</span><span class="sxs-lookup"><span data-stu-id="969d1-126">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="969d1-127">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="969d1-127">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="969d1-128">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span><span class="sxs-lookup"><span data-stu-id="969d1-128">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="969d1-129">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span><span class="sxs-lookup"><span data-stu-id="969d1-129">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="969d1-130">Getting started</span><span class="sxs-lookup"><span data-stu-id="969d1-130">Getting started</span></span>
<span data-ttu-id="969d1-131">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="969d1-131">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="969d1-132">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="969d1-132">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="969d1-133">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="969d1-133">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="969d1-134">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="969d1-134">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="969d1-135">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="969d1-135">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="969d1-136">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="969d1-136">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="969d1-137">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="969d1-137">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="969d1-138">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="969d1-138">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="969d1-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="969d1-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="969d1-140">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="969d1-140">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="969d1-141">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="969d1-141">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="969d1-142">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="969d1-142">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples) section of this article.</span></span>

<span data-ttu-id="969d1-143">The following sections provide details about JSON properties that are used to define Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="969d1-143">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="969d1-144">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="969d1-144">Linked service properties</span></span>
<span data-ttu-id="969d1-145">The following table provides description for JSON elements specific to Oracle linked service.</span><span class="sxs-lookup"><span data-stu-id="969d1-145">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="969d1-146">Property</span><span class="sxs-lookup"><span data-stu-id="969d1-146">Property</span></span> | <span data-ttu-id="969d1-147">Description</span><span class="sxs-lookup"><span data-stu-id="969d1-147">Description</span></span> | <span data-ttu-id="969d1-148">Required</span><span class="sxs-lookup"><span data-stu-id="969d1-148">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="969d1-149">type</span><span class="sxs-lookup"><span data-stu-id="969d1-149">type</span></span> |<span data-ttu-id="969d1-150">The type property must be set to: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="969d1-150">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="969d1-151">Yes</span><span class="sxs-lookup"><span data-stu-id="969d1-151">Yes</span></span> |
| <span data-ttu-id="969d1-152">driverType</span><span class="sxs-lookup"><span data-stu-id="969d1-152">driverType</span></span> | <span data-ttu-id="969d1-153">Specify which driver to use to copy data from/to Oracle Database.</span><span class="sxs-lookup"><span data-stu-id="969d1-153">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="969d1-154">Allowed values are **Microsoft** or **ODP** (default).</span><span class="sxs-lookup"><span data-stu-id="969d1-154">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="969d1-155">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span><span class="sxs-lookup"><span data-stu-id="969d1-155">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="969d1-156">No</span><span class="sxs-lookup"><span data-stu-id="969d1-156">No</span></span> |
| <span data-ttu-id="969d1-157">connectionString</span><span class="sxs-lookup"><span data-stu-id="969d1-157">connectionString</span></span> | <span data-ttu-id="969d1-158">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="969d1-158">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="969d1-159">Yes</span><span class="sxs-lookup"><span data-stu-id="969d1-159">Yes</span></span> |
| <span data-ttu-id="969d1-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="969d1-160">gatewayName</span></span> | <span data-ttu-id="969d1-161">Name of the gateway that that is used to connect to the on-premises Oracle server</span><span class="sxs-lookup"><span data-stu-id="969d1-161">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="969d1-162">Yes</span><span class="sxs-lookup"><span data-stu-id="969d1-162">Yes</span></span> |

<span data-ttu-id="969d1-163">**Example: using Microsoft driver:**</span><span class="sxs-lookup"><span data-stu-id="969d1-163">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="969d1-164">**Example: using ODP driver**</span><span class="sxs-lookup"><span data-stu-id="969d1-164">**Example: using ODP driver**</span></span>

<span data-ttu-id="969d1-165">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span><span class="sxs-lookup"><span data-stu-id="969d1-165">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="969d1-166">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="969d1-166">Dataset properties</span></span>
<span data-ttu-id="969d1-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="969d1-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="969d1-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="969d1-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="969d1-169">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="969d1-169">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="969d1-170">The typeProperties section for the dataset of type OracleTable has the following properties:</span><span class="sxs-lookup"><span data-stu-id="969d1-170">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="969d1-171">Property</span><span class="sxs-lookup"><span data-stu-id="969d1-171">Property</span></span> | <span data-ttu-id="969d1-172">Description</span><span class="sxs-lookup"><span data-stu-id="969d1-172">Description</span></span> | <span data-ttu-id="969d1-173">Required</span><span class="sxs-lookup"><span data-stu-id="969d1-173">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="969d1-174">tableName</span><span class="sxs-lookup"><span data-stu-id="969d1-174">tableName</span></span> |<span data-ttu-id="969d1-175">Name of the table in the Oracle Database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="969d1-175">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="969d1-176">No (if **oracleReaderQuery** of **OracleSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="969d1-176">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="969d1-177">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="969d1-177">Copy activity properties</span></span>
<span data-ttu-id="969d1-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="969d1-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="969d1-179">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="969d1-179">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="969d1-180">The Copy Activity takes only one input and produces only one output.</span><span class="sxs-lookup"><span data-stu-id="969d1-180">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="969d1-181">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="969d1-181">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="969d1-182">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="969d1-182">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="969d1-183">OracleSource</span><span class="sxs-lookup"><span data-stu-id="969d1-183">OracleSource</span></span>
<span data-ttu-id="969d1-184">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="969d1-184">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="969d1-185">Property</span><span class="sxs-lookup"><span data-stu-id="969d1-185">Property</span></span> | <span data-ttu-id="969d1-186">Description</span><span class="sxs-lookup"><span data-stu-id="969d1-186">Description</span></span> | <span data-ttu-id="969d1-187">Allowed values</span><span class="sxs-lookup"><span data-stu-id="969d1-187">Allowed values</span></span> | <span data-ttu-id="969d1-188">Required</span><span class="sxs-lookup"><span data-stu-id="969d1-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="969d1-189">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="969d1-189">oracleReaderQuery</span></span> |<span data-ttu-id="969d1-190">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="969d1-190">Use the custom query to read data.</span></span> |<span data-ttu-id="969d1-191">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="969d1-191">SQL query string.</span></span> <span data-ttu-id="969d1-192">For example: select \* from MyTable</span><span class="sxs-lookup"><span data-stu-id="969d1-192">For example: select \* from MyTable</span></span> <br/><br/><span data-ttu-id="969d1-193">If not specified, the SQL statement that is executed: select \* from MyTable</span><span class="sxs-lookup"><span data-stu-id="969d1-193">If not specified, the SQL statement that is executed: select \* from MyTable</span></span> |<span data-ttu-id="969d1-194">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="969d1-194">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="969d1-195">OracleSink</span><span class="sxs-lookup"><span data-stu-id="969d1-195">OracleSink</span></span>
<span data-ttu-id="969d1-196">**OracleSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="969d1-196">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="969d1-197">Property</span><span class="sxs-lookup"><span data-stu-id="969d1-197">Property</span></span> | <span data-ttu-id="969d1-198">Description</span><span class="sxs-lookup"><span data-stu-id="969d1-198">Description</span></span> | <span data-ttu-id="969d1-199">Allowed values</span><span class="sxs-lookup"><span data-stu-id="969d1-199">Allowed values</span></span> | <span data-ttu-id="969d1-200">Required</span><span class="sxs-lookup"><span data-stu-id="969d1-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="969d1-201">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="969d1-201">writeBatchTimeout</span></span> |<span data-ttu-id="969d1-202">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="969d1-202">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="969d1-203">timespan</span><span class="sxs-lookup"><span data-stu-id="969d1-203">timespan</span></span><br/><br/> <span data-ttu-id="969d1-204">Example: 00:30:00 (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="969d1-204">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="969d1-205">No</span><span class="sxs-lookup"><span data-stu-id="969d1-205">No</span></span> |
| <span data-ttu-id="969d1-206">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="969d1-206">writeBatchSize</span></span> |<span data-ttu-id="969d1-207">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="969d1-207">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="969d1-208">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="969d1-208">Integer (number of rows)</span></span> |<span data-ttu-id="969d1-209">No (default: 100)</span><span class="sxs-lookup"><span data-stu-id="969d1-209">No (default: 100)</span></span> |
| <span data-ttu-id="969d1-210">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="969d1-210">sqlWriterCleanupScript</span></span> |<span data-ttu-id="969d1-211">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="969d1-211">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="969d1-212">A query statement.</span><span class="sxs-lookup"><span data-stu-id="969d1-212">A query statement.</span></span> |<span data-ttu-id="969d1-213">No</span><span class="sxs-lookup"><span data-stu-id="969d1-213">No</span></span> |
| <span data-ttu-id="969d1-214">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="969d1-214">sliceIdentifierColumnName</span></span> |<span data-ttu-id="969d1-215">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="969d1-215">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="969d1-216">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="969d1-216">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="969d1-217">No</span><span class="sxs-lookup"><span data-stu-id="969d1-217">No</span></span> |

## <a name="json-examples"></a><span data-ttu-id="969d1-218">JSON examples</span><span class="sxs-lookup"><span data-stu-id="969d1-218">JSON examples</span></span>
<span data-ttu-id="969d1-219">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="969d1-219">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="969d1-220">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="969d1-220">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="969d1-221">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="969d1-221">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="969d1-222">Example: Copy data from Oracle to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="969d1-222">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="969d1-223">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="969d1-223">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="969d1-224">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="969d1-224">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="969d1-225">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="969d1-225">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="969d1-226">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="969d1-226">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="969d1-227">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="969d1-227">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="969d1-228">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span><span class="sxs-lookup"><span data-stu-id="969d1-228">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="969d1-229">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span><span class="sxs-lookup"><span data-stu-id="969d1-229">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="969d1-230">For more information on various properties used in the sample, see documentation in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="969d1-230">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="969d1-231">**Oracle linked service:**</span><span class="sxs-lookup"><span data-stu-id="969d1-231">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="969d1-232">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="969d1-232">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="969d1-233">**Oracle input dataset:**</span><span class="sxs-lookup"><span data-stu-id="969d1-233">**Oracle input dataset:**</span></span>

<span data-ttu-id="969d1-234">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="969d1-234">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="969d1-235">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="969d1-235">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
        },
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

<span data-ttu-id="969d1-236">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="969d1-236">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="969d1-237">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="969d1-237">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="969d1-238">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="969d1-238">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="969d1-239">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="969d1-239">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="969d1-240">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="969d1-240">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="969d1-241">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span><span class="sxs-lookup"><span data-stu-id="969d1-241">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="969d1-242">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="969d1-242">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="969d1-243">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="969d1-243">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="969d1-244">Example: Copy data from Azure Blob to Oracle</span><span class="sxs-lookup"><span data-stu-id="969d1-244">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="969d1-245">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span><span class="sxs-lookup"><span data-stu-id="969d1-245">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="969d1-246">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="969d1-246">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="969d1-247">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="969d1-247">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="969d1-248">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="969d1-248">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="969d1-249">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="969d1-249">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="969d1-250">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="969d1-250">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="969d1-251">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="969d1-251">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="969d1-252">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span><span class="sxs-lookup"><span data-stu-id="969d1-252">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="969d1-253">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span><span class="sxs-lookup"><span data-stu-id="969d1-253">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="969d1-254">For more information on various properties used in the sample, see documentation in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="969d1-254">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="969d1-255">**Oracle linked service:**</span><span class="sxs-lookup"><span data-stu-id="969d1-255">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="969d1-256">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="969d1-256">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="969d1-257">**Azure Blob input dataset**</span><span class="sxs-lookup"><span data-stu-id="969d1-257">**Azure Blob input dataset**</span></span>

<span data-ttu-id="969d1-258">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="969d1-258">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="969d1-259">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="969d1-259">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="969d1-260">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="969d1-260">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="969d1-261">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="969d1-261">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
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

<span data-ttu-id="969d1-262">**Oracle output dataset:**</span><span class="sxs-lookup"><span data-stu-id="969d1-262">**Oracle output dataset:**</span></span>

<span data-ttu-id="969d1-263">The sample assumes you have created a table “MyTable” in Oracle.</span><span class="sxs-lookup"><span data-stu-id="969d1-263">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="969d1-264">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="969d1-264">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="969d1-265">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="969d1-265">New rows are added to the table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="969d1-266">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="969d1-266">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="969d1-267">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="969d1-267">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="969d1-268">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="969d1-268">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="969d1-269">Troubleshooting tips</span><span class="sxs-lookup"><span data-stu-id="969d1-269">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="969d1-270">Problem 1: .NET Framework Data Provider</span><span class="sxs-lookup"><span data-stu-id="969d1-270">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="969d1-271">You see the following **error message**:</span><span class="sxs-lookup"><span data-stu-id="969d1-271">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="969d1-272">**Possible causes:**</span><span class="sxs-lookup"><span data-stu-id="969d1-272">**Possible causes:**</span></span>

1. <span data-ttu-id="969d1-273">The .NET Framework Data Provider for Oracle was not installed.</span><span class="sxs-lookup"><span data-stu-id="969d1-273">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="969d1-274">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span><span class="sxs-lookup"><span data-stu-id="969d1-274">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="969d1-275">**Resolution/Workaround:**</span><span class="sxs-lookup"><span data-stu-id="969d1-275">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="969d1-276">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span><span class="sxs-lookup"><span data-stu-id="969d1-276">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="969d1-277">If you get the error message even after installing the provider, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="969d1-277">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="969d1-278">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="969d1-278">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="969d1-279">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="969d1-279">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="969d1-280">”</span><span class="sxs-lookup"><span data-stu-id="969d1-280">”</span></span>
3. <span data-ttu-id="969d1-281">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="969d1-281">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="969d1-282">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span><span class="sxs-lookup"><span data-stu-id="969d1-282">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="969d1-283">Problem 2: datetime formatting</span><span class="sxs-lookup"><span data-stu-id="969d1-283">Problem 2: datetime formatting</span></span>

<span data-ttu-id="969d1-284">You see the following **error message**:</span><span class="sxs-lookup"><span data-stu-id="969d1-284">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="969d1-285">**Resolution/Workaround:**</span><span class="sxs-lookup"><span data-stu-id="969d1-285">**Resolution/Workaround:**</span></span>

<span data-ttu-id="969d1-286">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span><span class="sxs-lookup"><span data-stu-id="969d1-286">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


### <a name="type-mapping-for-oracle"></a><span data-ttu-id="969d1-287">Type mapping for Oracle</span><span class="sxs-lookup"><span data-stu-id="969d1-287">Type mapping for Oracle</span></span>
<span data-ttu-id="969d1-288">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="969d1-288">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="969d1-289">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="969d1-289">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="969d1-290">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="969d1-290">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="969d1-291">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="969d1-291">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="969d1-292">Oracle data type</span><span class="sxs-lookup"><span data-stu-id="969d1-292">Oracle data type</span></span> | <span data-ttu-id="969d1-293">.NET Framework data type</span><span class="sxs-lookup"><span data-stu-id="969d1-293">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="969d1-294">BFILE</span><span class="sxs-lookup"><span data-stu-id="969d1-294">BFILE</span></span> |<span data-ttu-id="969d1-295">Byte[]</span><span class="sxs-lookup"><span data-stu-id="969d1-295">Byte[]</span></span> |
| <span data-ttu-id="969d1-296">BLOB</span><span class="sxs-lookup"><span data-stu-id="969d1-296">BLOB</span></span> |<span data-ttu-id="969d1-297">Byte[]</span><span class="sxs-lookup"><span data-stu-id="969d1-297">Byte[]</span></span> |
| <span data-ttu-id="969d1-298">CHAR</span><span class="sxs-lookup"><span data-stu-id="969d1-298">CHAR</span></span> |<span data-ttu-id="969d1-299">String</span><span class="sxs-lookup"><span data-stu-id="969d1-299">String</span></span> |
| <span data-ttu-id="969d1-300">CLOB</span><span class="sxs-lookup"><span data-stu-id="969d1-300">CLOB</span></span> |<span data-ttu-id="969d1-301">String</span><span class="sxs-lookup"><span data-stu-id="969d1-301">String</span></span> |
| <span data-ttu-id="969d1-302">DATE</span><span class="sxs-lookup"><span data-stu-id="969d1-302">DATE</span></span> |<span data-ttu-id="969d1-303">DateTime</span><span class="sxs-lookup"><span data-stu-id="969d1-303">DateTime</span></span> |
| <span data-ttu-id="969d1-304">FLOAT</span><span class="sxs-lookup"><span data-stu-id="969d1-304">FLOAT</span></span> |<span data-ttu-id="969d1-305">Decimal</span><span class="sxs-lookup"><span data-stu-id="969d1-305">Decimal</span></span> |
| <span data-ttu-id="969d1-306">INTEGER</span><span class="sxs-lookup"><span data-stu-id="969d1-306">INTEGER</span></span> |<span data-ttu-id="969d1-307">Decimal</span><span class="sxs-lookup"><span data-stu-id="969d1-307">Decimal</span></span> |
| <span data-ttu-id="969d1-308">INTERVAL YEAR TO MONTH</span><span class="sxs-lookup"><span data-stu-id="969d1-308">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="969d1-309">Int32</span><span class="sxs-lookup"><span data-stu-id="969d1-309">Int32</span></span> |
| <span data-ttu-id="969d1-310">INTERVAL DAY TO SECOND</span><span class="sxs-lookup"><span data-stu-id="969d1-310">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="969d1-311">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="969d1-311">TimeSpan</span></span> |
| <span data-ttu-id="969d1-312">LONG</span><span class="sxs-lookup"><span data-stu-id="969d1-312">LONG</span></span> |<span data-ttu-id="969d1-313">String</span><span class="sxs-lookup"><span data-stu-id="969d1-313">String</span></span> |
| <span data-ttu-id="969d1-314">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="969d1-314">LONG RAW</span></span> |<span data-ttu-id="969d1-315">Byte[]</span><span class="sxs-lookup"><span data-stu-id="969d1-315">Byte[]</span></span> |
| <span data-ttu-id="969d1-316">NCHAR</span><span class="sxs-lookup"><span data-stu-id="969d1-316">NCHAR</span></span> |<span data-ttu-id="969d1-317">String</span><span class="sxs-lookup"><span data-stu-id="969d1-317">String</span></span> |
| <span data-ttu-id="969d1-318">NCLOB</span><span class="sxs-lookup"><span data-stu-id="969d1-318">NCLOB</span></span> |<span data-ttu-id="969d1-319">String</span><span class="sxs-lookup"><span data-stu-id="969d1-319">String</span></span> |
| <span data-ttu-id="969d1-320">NUMBER</span><span class="sxs-lookup"><span data-stu-id="969d1-320">NUMBER</span></span> |<span data-ttu-id="969d1-321">Decimal</span><span class="sxs-lookup"><span data-stu-id="969d1-321">Decimal</span></span> |
| <span data-ttu-id="969d1-322">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="969d1-322">NVARCHAR2</span></span> |<span data-ttu-id="969d1-323">String</span><span class="sxs-lookup"><span data-stu-id="969d1-323">String</span></span> |
| <span data-ttu-id="969d1-324">RAW</span><span class="sxs-lookup"><span data-stu-id="969d1-324">RAW</span></span> |<span data-ttu-id="969d1-325">Byte[]</span><span class="sxs-lookup"><span data-stu-id="969d1-325">Byte[]</span></span> |
| <span data-ttu-id="969d1-326">ROWID</span><span class="sxs-lookup"><span data-stu-id="969d1-326">ROWID</span></span> |<span data-ttu-id="969d1-327">String</span><span class="sxs-lookup"><span data-stu-id="969d1-327">String</span></span> |
| <span data-ttu-id="969d1-328">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="969d1-328">TIMESTAMP</span></span> |<span data-ttu-id="969d1-329">DateTime</span><span class="sxs-lookup"><span data-stu-id="969d1-329">DateTime</span></span> |
| <span data-ttu-id="969d1-330">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="969d1-330">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="969d1-331">DateTime</span><span class="sxs-lookup"><span data-stu-id="969d1-331">DateTime</span></span> |
| <span data-ttu-id="969d1-332">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="969d1-332">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="969d1-333">DateTime</span><span class="sxs-lookup"><span data-stu-id="969d1-333">DateTime</span></span> |
| <span data-ttu-id="969d1-334">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="969d1-334">UNSIGNED INTEGER</span></span> |<span data-ttu-id="969d1-335">Number</span><span class="sxs-lookup"><span data-stu-id="969d1-335">Number</span></span> |
| <span data-ttu-id="969d1-336">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="969d1-336">VARCHAR2</span></span> |<span data-ttu-id="969d1-337">String</span><span class="sxs-lookup"><span data-stu-id="969d1-337">String</span></span> |
| <span data-ttu-id="969d1-338">XML</span><span class="sxs-lookup"><span data-stu-id="969d1-338">XML</span></span> |<span data-ttu-id="969d1-339">String</span><span class="sxs-lookup"><span data-stu-id="969d1-339">String</span></span> |

> [!NOTE]
> <span data-ttu-id="969d1-340">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span><span class="sxs-lookup"><span data-stu-id="969d1-340">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="969d1-341">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="969d1-341">Map source to sink columns</span></span>
<span data-ttu-id="969d1-342">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="969d1-342">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="969d1-343">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="969d1-343">Repeatable read from relational sources</span></span>
<span data-ttu-id="969d1-344">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="969d1-344">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="969d1-345">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="969d1-345">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="969d1-346">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="969d1-346">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="969d1-347">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="969d1-347">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="969d1-348">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="969d1-348">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="969d1-349">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="969d1-349">Performance and Tuning</span></span>
<span data-ttu-id="969d1-350">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="969d1-350">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
