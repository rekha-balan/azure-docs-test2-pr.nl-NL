---
title: Copy data to or from Oracle using Data Factory | Microsoft Docs
description: Learn how to copy data to/from Oracle database that is on-premises using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/15/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 10535e75a32a9f95e759340cf14d693f43639473
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864465"
---
# <a name="copy-data-to-or-from-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="1464d-103">Copy data to or from on-premises Oracle using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1464d-103">Copy data to or from on-premises Oracle using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-onprem-oracle-connector.md)
> * [Version 2 (current version)](../connector-oracle.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Oracle connector in V2](../connector-oracle.md).


<span data-ttu-id="1464d-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span><span class="sxs-lookup"><span data-stu-id="1464d-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="1464d-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1464d-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="1464d-110">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="1464d-110">Supported scenarios</span></span>
<span data-ttu-id="1464d-111">You can copy data **from an Oracle database** to the following data stores:</span><span class="sxs-lookup"><span data-stu-id="1464d-111">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="1464d-112">You can copy data from the following data stores **to an Oracle database**:</span><span class="sxs-lookup"><span data-stu-id="1464d-112">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="1464d-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1464d-113">Prerequisites</span></span>
<span data-ttu-id="1464d-114">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="1464d-114">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="1464d-115">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span><span class="sxs-lookup"><span data-stu-id="1464d-115">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="1464d-116">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="1464d-116">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="1464d-117">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="1464d-117">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.

## <a name="supported-versions-and-installation"></a><span data-ttu-id="1464d-119">Supported versions and installation</span><span class="sxs-lookup"><span data-stu-id="1464d-119">Supported versions and installation</span></span>
<span data-ttu-id="1464d-120">This Oracle connector support two versions of drivers:</span><span class="sxs-lookup"><span data-stu-id="1464d-120">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="1464d-121">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span><span class="sxs-lookup"><span data-stu-id="1464d-121">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="1464d-122">Below versions of Oracle databases are supported:</span><span class="sxs-lookup"><span data-stu-id="1464d-122">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="1464d-123">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="1464d-123">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="1464d-124">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="1464d-124">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="1464d-125">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="1464d-125">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="1464d-126">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="1464d-126">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="1464d-127">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="1464d-127">Oracle 8i R3 (8.1.7)</span></span>

> [!NOTE]
> Oracle proxy server is not supported.

> [!IMPORTANT]
> Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle. And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver. Alternatively, you can use the copy wizard to validate the connectivity.
>

- <span data-ttu-id="1464d-132">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span><span class="sxs-lookup"><span data-stu-id="1464d-132">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="1464d-133">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1464d-133">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="1464d-134">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span><span class="sxs-lookup"><span data-stu-id="1464d-134">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="1464d-135">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span><span class="sxs-lookup"><span data-stu-id="1464d-135">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="1464d-136">If you choose “XCopy Installation”, follow steps in the readme.htm.</span><span class="sxs-lookup"><span data-stu-id="1464d-136">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="1464d-137">We recommend you choose the installer with UI (non-XCopy one).</span><span class="sxs-lookup"><span data-stu-id="1464d-137">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="1464d-138">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="1464d-138">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="1464d-139">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span><span class="sxs-lookup"><span data-stu-id="1464d-139">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="1464d-140">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span><span class="sxs-lookup"><span data-stu-id="1464d-140">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1464d-141">Getting started</span><span class="sxs-lookup"><span data-stu-id="1464d-141">Getting started</span></span>
<span data-ttu-id="1464d-142">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="1464d-142">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="1464d-143">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="1464d-143">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1464d-144">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="1464d-144">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="1464d-145">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="1464d-145">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1464d-146">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="1464d-146">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="1464d-147">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="1464d-147">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="1464d-148">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="1464d-148">Create a **data factory**.</span></span> <span data-ttu-id="1464d-149">A data factory may contain one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="1464d-149">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="1464d-150">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="1464d-150">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="1464d-151">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="1464d-151">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="1464d-152">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="1464d-152">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="1464d-153">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="1464d-153">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="1464d-154">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="1464d-154">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="1464d-155">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span><span class="sxs-lookup"><span data-stu-id="1464d-155">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="1464d-156">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="1464d-156">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="1464d-157">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="1464d-157">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="1464d-158">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1464d-158">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="1464d-159">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span><span class="sxs-lookup"><span data-stu-id="1464d-159">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="1464d-160">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="1464d-160">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="1464d-161">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span><span class="sxs-lookup"><span data-stu-id="1464d-161">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="1464d-162">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="1464d-162">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1464d-163">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="1464d-163">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="1464d-164">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span><span class="sxs-lookup"><span data-stu-id="1464d-164">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="1464d-165">The following sections provide details about JSON properties that are used to define Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="1464d-165">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1464d-166">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="1464d-166">Linked service properties</span></span>
<span data-ttu-id="1464d-167">The following table provides description for JSON elements specific to Oracle linked service.</span><span class="sxs-lookup"><span data-stu-id="1464d-167">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="1464d-168">Property</span><span class="sxs-lookup"><span data-stu-id="1464d-168">Property</span></span> | <span data-ttu-id="1464d-169">Description</span><span class="sxs-lookup"><span data-stu-id="1464d-169">Description</span></span> | <span data-ttu-id="1464d-170">Required</span><span class="sxs-lookup"><span data-stu-id="1464d-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1464d-171">type</span><span class="sxs-lookup"><span data-stu-id="1464d-171">type</span></span> |<span data-ttu-id="1464d-172">The type property must be set to: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="1464d-172">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="1464d-173">Yes</span><span class="sxs-lookup"><span data-stu-id="1464d-173">Yes</span></span> |
| <span data-ttu-id="1464d-174">driverType</span><span class="sxs-lookup"><span data-stu-id="1464d-174">driverType</span></span> | <span data-ttu-id="1464d-175">Specify which driver to use to copy data from/to Oracle Database.</span><span class="sxs-lookup"><span data-stu-id="1464d-175">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="1464d-176">Allowed values are **Microsoft** or **ODP** (default).</span><span class="sxs-lookup"><span data-stu-id="1464d-176">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="1464d-177">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span><span class="sxs-lookup"><span data-stu-id="1464d-177">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="1464d-178">No</span><span class="sxs-lookup"><span data-stu-id="1464d-178">No</span></span> |
| <span data-ttu-id="1464d-179">connectionString</span><span class="sxs-lookup"><span data-stu-id="1464d-179">connectionString</span></span> | <span data-ttu-id="1464d-180">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="1464d-180">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="1464d-181">Yes</span><span class="sxs-lookup"><span data-stu-id="1464d-181">Yes</span></span> |
| <span data-ttu-id="1464d-182">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1464d-182">gatewayName</span></span> | <span data-ttu-id="1464d-183">Name of the gateway that is used to connect to the on-premises Oracle server</span><span class="sxs-lookup"><span data-stu-id="1464d-183">Name of the gateway that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="1464d-184">Yes</span><span class="sxs-lookup"><span data-stu-id="1464d-184">Yes</span></span> |

<span data-ttu-id="1464d-185">**Example: using Microsoft driver:**</span><span class="sxs-lookup"><span data-stu-id="1464d-185">**Example: using Microsoft driver:**</span></span>

>[!TIP]
>If you hit error saying "ORA-01025: UPI parameter out of range" and your Oracle is of version 8i, add `WireProtocolMode=1` to your connection string and try again.

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

<span data-ttu-id="1464d-187">**Example: using ODP driver**</span><span class="sxs-lookup"><span data-stu-id="1464d-187">**Example: using ODP driver**</span></span>

<span data-ttu-id="1464d-188">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span><span class="sxs-lookup"><span data-stu-id="1464d-188">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="1464d-189">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="1464d-189">Dataset properties</span></span>
<span data-ttu-id="1464d-190">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="1464d-190">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1464d-191">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="1464d-191">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1464d-192">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="1464d-192">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="1464d-193">The typeProperties section for the dataset of type OracleTable has the following properties:</span><span class="sxs-lookup"><span data-stu-id="1464d-193">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="1464d-194">Property</span><span class="sxs-lookup"><span data-stu-id="1464d-194">Property</span></span> | <span data-ttu-id="1464d-195">Description</span><span class="sxs-lookup"><span data-stu-id="1464d-195">Description</span></span> | <span data-ttu-id="1464d-196">Required</span><span class="sxs-lookup"><span data-stu-id="1464d-196">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1464d-197">tableName</span><span class="sxs-lookup"><span data-stu-id="1464d-197">tableName</span></span> |<span data-ttu-id="1464d-198">Name of the table in the Oracle Database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="1464d-198">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="1464d-199">No (if **oracleReaderQuery** of **OracleSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="1464d-199">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="1464d-200">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="1464d-200">Copy activity properties</span></span>
<span data-ttu-id="1464d-201">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="1464d-201">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1464d-202">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="1464d-202">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> The Copy Activity takes only one input and produces only one output.

<span data-ttu-id="1464d-204">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="1464d-204">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="1464d-205">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="1464d-205">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="1464d-206">OracleSource</span><span class="sxs-lookup"><span data-stu-id="1464d-206">OracleSource</span></span>
<span data-ttu-id="1464d-207">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="1464d-207">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="1464d-208">Property</span><span class="sxs-lookup"><span data-stu-id="1464d-208">Property</span></span> | <span data-ttu-id="1464d-209">Description</span><span class="sxs-lookup"><span data-stu-id="1464d-209">Description</span></span> | <span data-ttu-id="1464d-210">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1464d-210">Allowed values</span></span> | <span data-ttu-id="1464d-211">Required</span><span class="sxs-lookup"><span data-stu-id="1464d-211">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1464d-212">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="1464d-212">oracleReaderQuery</span></span> |<span data-ttu-id="1464d-213">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="1464d-213">Use the custom query to read data.</span></span> |<span data-ttu-id="1464d-214">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="1464d-214">SQL query string.</span></span> <span data-ttu-id="1464d-215">For example: select \* from MyTable</span><span class="sxs-lookup"><span data-stu-id="1464d-215">For example: select \* from MyTable</span></span> <br/><br/><span data-ttu-id="1464d-216">If not specified, the SQL statement that is executed: select \* from MyTable</span><span class="sxs-lookup"><span data-stu-id="1464d-216">If not specified, the SQL statement that is executed: select \* from MyTable</span></span> |<span data-ttu-id="1464d-217">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="1464d-217">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="1464d-218">OracleSink</span><span class="sxs-lookup"><span data-stu-id="1464d-218">OracleSink</span></span>
<span data-ttu-id="1464d-219">**OracleSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="1464d-219">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="1464d-220">Property</span><span class="sxs-lookup"><span data-stu-id="1464d-220">Property</span></span> | <span data-ttu-id="1464d-221">Description</span><span class="sxs-lookup"><span data-stu-id="1464d-221">Description</span></span> | <span data-ttu-id="1464d-222">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1464d-222">Allowed values</span></span> | <span data-ttu-id="1464d-223">Required</span><span class="sxs-lookup"><span data-stu-id="1464d-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1464d-224">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1464d-224">writeBatchTimeout</span></span> |<span data-ttu-id="1464d-225">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="1464d-225">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="1464d-226">timespan</span><span class="sxs-lookup"><span data-stu-id="1464d-226">timespan</span></span><br/><br/> <span data-ttu-id="1464d-227">Example: 00:30:00 (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="1464d-227">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="1464d-228">No</span><span class="sxs-lookup"><span data-stu-id="1464d-228">No</span></span> |
| <span data-ttu-id="1464d-229">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1464d-229">writeBatchSize</span></span> |<span data-ttu-id="1464d-230">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="1464d-230">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="1464d-231">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="1464d-231">Integer (number of rows)</span></span> |<span data-ttu-id="1464d-232">No (default: 100)</span><span class="sxs-lookup"><span data-stu-id="1464d-232">No (default: 100)</span></span> |
| <span data-ttu-id="1464d-233">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="1464d-233">sqlWriterCleanupScript</span></span> |<span data-ttu-id="1464d-234">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="1464d-234">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="1464d-235">A query statement.</span><span class="sxs-lookup"><span data-stu-id="1464d-235">A query statement.</span></span> |<span data-ttu-id="1464d-236">No</span><span class="sxs-lookup"><span data-stu-id="1464d-236">No</span></span> |
| <span data-ttu-id="1464d-237">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="1464d-237">sliceIdentifierColumnName</span></span> |<span data-ttu-id="1464d-238">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="1464d-238">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="1464d-239">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="1464d-239">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="1464d-240">No</span><span class="sxs-lookup"><span data-stu-id="1464d-240">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="1464d-241">JSON examples for copying data to and from Oracle database</span><span class="sxs-lookup"><span data-stu-id="1464d-241">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="1464d-242">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1464d-242">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1464d-243">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1464d-243">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="1464d-244">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1464d-244">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="1464d-245">Example: Copy data from Oracle to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1464d-245">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="1464d-246">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="1464d-246">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="1464d-247">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1464d-247">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="1464d-248">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1464d-248">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1464d-249">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1464d-249">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="1464d-250">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1464d-250">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1464d-251">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span><span class="sxs-lookup"><span data-stu-id="1464d-251">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="1464d-252">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span><span class="sxs-lookup"><span data-stu-id="1464d-252">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="1464d-253">For more information on various properties used in the sample, see documentation in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="1464d-253">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="1464d-254">**Oracle linked service:**</span><span class="sxs-lookup"><span data-stu-id="1464d-254">**Oracle linked service:**</span></span>

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

<span data-ttu-id="1464d-255">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="1464d-255">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="1464d-256">**Oracle input dataset:**</span><span class="sxs-lookup"><span data-stu-id="1464d-256">**Oracle input dataset:**</span></span>

<span data-ttu-id="1464d-257">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="1464d-257">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="1464d-258">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="1464d-258">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="1464d-259">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="1464d-259">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="1464d-260">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1464d-260">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1464d-261">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="1464d-261">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1464d-262">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="1464d-262">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="1464d-263">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="1464d-263">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="1464d-264">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span><span class="sxs-lookup"><span data-stu-id="1464d-264">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="1464d-265">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1464d-265">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="1464d-266">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="1464d-266">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="1464d-267">Example: Copy data from Azure Blob to Oracle</span><span class="sxs-lookup"><span data-stu-id="1464d-267">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="1464d-268">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span><span class="sxs-lookup"><span data-stu-id="1464d-268">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="1464d-269">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1464d-269">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="1464d-270">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="1464d-270">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="1464d-271">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1464d-271">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="1464d-272">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1464d-272">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1464d-273">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1464d-273">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="1464d-274">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1464d-274">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1464d-275">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span><span class="sxs-lookup"><span data-stu-id="1464d-275">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="1464d-276">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span><span class="sxs-lookup"><span data-stu-id="1464d-276">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="1464d-277">For more information on various properties used in the sample, see documentation in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="1464d-277">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="1464d-278">**Oracle linked service:**</span><span class="sxs-lookup"><span data-stu-id="1464d-278">**Oracle linked service:**</span></span>
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

<span data-ttu-id="1464d-279">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="1464d-279">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="1464d-280">**Azure Blob input dataset**</span><span class="sxs-lookup"><span data-stu-id="1464d-280">**Azure Blob input dataset**</span></span>

<span data-ttu-id="1464d-281">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1464d-281">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1464d-282">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="1464d-282">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1464d-283">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="1464d-283">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="1464d-284">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="1464d-284">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="1464d-285">**Oracle output dataset:**</span><span class="sxs-lookup"><span data-stu-id="1464d-285">**Oracle output dataset:**</span></span>

<span data-ttu-id="1464d-286">The sample assumes you have created a table “MyTable” in Oracle.</span><span class="sxs-lookup"><span data-stu-id="1464d-286">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="1464d-287">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="1464d-287">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="1464d-288">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="1464d-288">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="1464d-289">**Pipeline with Copy activity:**</span><span class="sxs-lookup"><span data-stu-id="1464d-289">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="1464d-290">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="1464d-290">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1464d-291">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="1464d-291">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="1464d-292">Troubleshooting tips</span><span class="sxs-lookup"><span data-stu-id="1464d-292">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="1464d-293">Problem 1: .NET Framework Data Provider</span><span class="sxs-lookup"><span data-stu-id="1464d-293">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="1464d-294">You see the following **error message**:</span><span class="sxs-lookup"><span data-stu-id="1464d-294">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="1464d-295">**Possible causes:**</span><span class="sxs-lookup"><span data-stu-id="1464d-295">**Possible causes:**</span></span>

1. <span data-ttu-id="1464d-296">The .NET Framework Data Provider for Oracle was not installed.</span><span class="sxs-lookup"><span data-stu-id="1464d-296">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="1464d-297">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span><span class="sxs-lookup"><span data-stu-id="1464d-297">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="1464d-298">**Resolution/Workaround:**</span><span class="sxs-lookup"><span data-stu-id="1464d-298">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="1464d-299">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span><span class="sxs-lookup"><span data-stu-id="1464d-299">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="1464d-300">If you get the error message even after installing the provider, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="1464d-300">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="1464d-301">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="1464d-301">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="1464d-302">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="1464d-302">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="1464d-303">”</span><span class="sxs-lookup"><span data-stu-id="1464d-303">”</span></span>
3. <span data-ttu-id="1464d-304">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="1464d-304">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="1464d-305">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span><span class="sxs-lookup"><span data-stu-id="1464d-305">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="1464d-306">Problem 2: datetime formatting</span><span class="sxs-lookup"><span data-stu-id="1464d-306">Problem 2: datetime formatting</span></span>

<span data-ttu-id="1464d-307">You see the following **error message**:</span><span class="sxs-lookup"><span data-stu-id="1464d-307">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="1464d-308">**Resolution/Workaround:**</span><span class="sxs-lookup"><span data-stu-id="1464d-308">**Resolution/Workaround:**</span></span>

<span data-ttu-id="1464d-309">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span><span class="sxs-lookup"><span data-stu-id="1464d-309">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="1464d-310">Type mapping for Oracle</span><span class="sxs-lookup"><span data-stu-id="1464d-310">Type mapping for Oracle</span></span>
<span data-ttu-id="1464d-311">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="1464d-311">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="1464d-312">Convert from native source types to .NET type</span><span class="sxs-lookup"><span data-stu-id="1464d-312">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="1464d-313">Convert from .NET type to native sink type</span><span class="sxs-lookup"><span data-stu-id="1464d-313">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="1464d-314">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span><span class="sxs-lookup"><span data-stu-id="1464d-314">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="1464d-315">Oracle data type</span><span class="sxs-lookup"><span data-stu-id="1464d-315">Oracle data type</span></span> | <span data-ttu-id="1464d-316">.NET Framework data type</span><span class="sxs-lookup"><span data-stu-id="1464d-316">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="1464d-317">BFILE</span><span class="sxs-lookup"><span data-stu-id="1464d-317">BFILE</span></span> |<span data-ttu-id="1464d-318">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1464d-318">Byte[]</span></span> |
| <span data-ttu-id="1464d-319">BLOB</span><span class="sxs-lookup"><span data-stu-id="1464d-319">BLOB</span></span> |<span data-ttu-id="1464d-320">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1464d-320">Byte[]</span></span><br/><span data-ttu-id="1464d-321">(only supported on Oracle 10g and higher when using Microsoft driver)</span><span class="sxs-lookup"><span data-stu-id="1464d-321">(only supported on Oracle 10g and higher when using Microsoft driver)</span></span> |
| <span data-ttu-id="1464d-322">CHAR</span><span class="sxs-lookup"><span data-stu-id="1464d-322">CHAR</span></span> |<span data-ttu-id="1464d-323">String</span><span class="sxs-lookup"><span data-stu-id="1464d-323">String</span></span> |
| <span data-ttu-id="1464d-324">CLOB</span><span class="sxs-lookup"><span data-stu-id="1464d-324">CLOB</span></span> |<span data-ttu-id="1464d-325">String</span><span class="sxs-lookup"><span data-stu-id="1464d-325">String</span></span> |
| <span data-ttu-id="1464d-326">DATE</span><span class="sxs-lookup"><span data-stu-id="1464d-326">DATE</span></span> |<span data-ttu-id="1464d-327">DateTime</span><span class="sxs-lookup"><span data-stu-id="1464d-327">DateTime</span></span> |
| <span data-ttu-id="1464d-328">FLOAT</span><span class="sxs-lookup"><span data-stu-id="1464d-328">FLOAT</span></span> |<span data-ttu-id="1464d-329">Decimal, String (if precision > 28)</span><span class="sxs-lookup"><span data-stu-id="1464d-329">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="1464d-330">INTEGER</span><span class="sxs-lookup"><span data-stu-id="1464d-330">INTEGER</span></span> |<span data-ttu-id="1464d-331">Decimal, String (if precision > 28)</span><span class="sxs-lookup"><span data-stu-id="1464d-331">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="1464d-332">INTERVAL YEAR TO MONTH</span><span class="sxs-lookup"><span data-stu-id="1464d-332">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="1464d-333">Int32</span><span class="sxs-lookup"><span data-stu-id="1464d-333">Int32</span></span> |
| <span data-ttu-id="1464d-334">INTERVAL DAY TO SECOND</span><span class="sxs-lookup"><span data-stu-id="1464d-334">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="1464d-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1464d-335">TimeSpan</span></span> |
| <span data-ttu-id="1464d-336">LONG</span><span class="sxs-lookup"><span data-stu-id="1464d-336">LONG</span></span> |<span data-ttu-id="1464d-337">String</span><span class="sxs-lookup"><span data-stu-id="1464d-337">String</span></span> |
| <span data-ttu-id="1464d-338">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="1464d-338">LONG RAW</span></span> |<span data-ttu-id="1464d-339">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1464d-339">Byte[]</span></span> |
| <span data-ttu-id="1464d-340">NCHAR</span><span class="sxs-lookup"><span data-stu-id="1464d-340">NCHAR</span></span> |<span data-ttu-id="1464d-341">String</span><span class="sxs-lookup"><span data-stu-id="1464d-341">String</span></span> |
| <span data-ttu-id="1464d-342">NCLOB</span><span class="sxs-lookup"><span data-stu-id="1464d-342">NCLOB</span></span> |<span data-ttu-id="1464d-343">String</span><span class="sxs-lookup"><span data-stu-id="1464d-343">String</span></span> |
| <span data-ttu-id="1464d-344">NUMBER</span><span class="sxs-lookup"><span data-stu-id="1464d-344">NUMBER</span></span> |<span data-ttu-id="1464d-345">Decimal, String (if precision > 28)</span><span class="sxs-lookup"><span data-stu-id="1464d-345">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="1464d-346">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="1464d-346">NVARCHAR2</span></span> |<span data-ttu-id="1464d-347">String</span><span class="sxs-lookup"><span data-stu-id="1464d-347">String</span></span> |
| <span data-ttu-id="1464d-348">RAW</span><span class="sxs-lookup"><span data-stu-id="1464d-348">RAW</span></span> |<span data-ttu-id="1464d-349">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1464d-349">Byte[]</span></span> |
| <span data-ttu-id="1464d-350">ROWID</span><span class="sxs-lookup"><span data-stu-id="1464d-350">ROWID</span></span> |<span data-ttu-id="1464d-351">String</span><span class="sxs-lookup"><span data-stu-id="1464d-351">String</span></span> |
| <span data-ttu-id="1464d-352">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="1464d-352">TIMESTAMP</span></span> |<span data-ttu-id="1464d-353">DateTime</span><span class="sxs-lookup"><span data-stu-id="1464d-353">DateTime</span></span> |
| <span data-ttu-id="1464d-354">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="1464d-354">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="1464d-355">DateTime</span><span class="sxs-lookup"><span data-stu-id="1464d-355">DateTime</span></span> |
| <span data-ttu-id="1464d-356">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="1464d-356">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="1464d-357">DateTime</span><span class="sxs-lookup"><span data-stu-id="1464d-357">DateTime</span></span> |
| <span data-ttu-id="1464d-358">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="1464d-358">UNSIGNED INTEGER</span></span> |<span data-ttu-id="1464d-359">Number</span><span class="sxs-lookup"><span data-stu-id="1464d-359">Number</span></span> |
| <span data-ttu-id="1464d-360">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="1464d-360">VARCHAR2</span></span> |<span data-ttu-id="1464d-361">String</span><span class="sxs-lookup"><span data-stu-id="1464d-361">String</span></span> |
| <span data-ttu-id="1464d-362">XML</span><span class="sxs-lookup"><span data-stu-id="1464d-362">XML</span></span> |<span data-ttu-id="1464d-363">String</span><span class="sxs-lookup"><span data-stu-id="1464d-363">String</span></span> |

> [!NOTE]
> Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="1464d-365">Map source to sink columns</span><span class="sxs-lookup"><span data-stu-id="1464d-365">Map source to sink columns</span></span>
<span data-ttu-id="1464d-366">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1464d-366">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1464d-367">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="1464d-367">Repeatable read from relational sources</span></span>
<span data-ttu-id="1464d-368">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="1464d-368">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="1464d-369">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="1464d-369">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1464d-370">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="1464d-370">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1464d-371">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="1464d-371">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="1464d-372">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="1464d-372">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1464d-373">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="1464d-373">Performance and Tuning</span></span>
<span data-ttu-id="1464d-374">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="1464d-374">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
