---
title: Copy data from SAP HANA using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from SAP HANA to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 02/07/2018
ms.author: jingwang
ms.openlocfilehash: 1ded69225319e447ad210aed267741b2803889ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855696"
---
# <a name="copy-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="0a5f2-103">Copy data from SAP HANA using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0a5f2-103">Copy data from SAP HANA using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-sap-hana-connector.md)
> * [Current version](connector-sap-hana.md)

<span data-ttu-id="0a5f2-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an SAP HANA database.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an SAP HANA database.</span></span> <span data-ttu-id="0a5f2-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="0a5f2-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="0a5f2-108">Supported capabilities</span></span>

<span data-ttu-id="0a5f2-109">You can copy data from SAP HANA database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-109">You can copy data from SAP HANA database to any supported sink data store.</span></span> <span data-ttu-id="0a5f2-110">For a list of data stores supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-110">For a list of data stores supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="0a5f2-111">Specifically, this SAP HANA connector supports:</span><span class="sxs-lookup"><span data-stu-id="0a5f2-111">Specifically, this SAP HANA connector supports:</span></span>

- <span data-ttu-id="0a5f2-112">Copying data from any version of SAP HANA database.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-112">Copying data from any version of SAP HANA database.</span></span>
- <span data-ttu-id="0a5f2-113">Copying data from **HANA information models** (such as Analytic and Calculation views) and **Row/Column tables** using SQL queries.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-113">Copying data from **HANA information models** (such as Analytic and Calculation views) and **Row/Column tables** using SQL queries.</span></span>
- <span data-ttu-id="0a5f2-114">Copying data using **Basic** or **Windows** authentication.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-114">Copying data using **Basic** or **Windows** authentication.</span></span>

> [!NOTE]
> To copy data **into** SAP HANA data store, use generic ODBC connector. See [SAP HANA sink](connector-odbc.md#sap-hana-sink) with details. Note the linked services for SAP HANA connector and ODBC connector are with different type thus cannot be reused.

## <a name="prerequisites"></a><span data-ttu-id="0a5f2-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0a5f2-118">Prerequisites</span></span>

<span data-ttu-id="0a5f2-119">To use this SAP HANA connector, you need to:</span><span class="sxs-lookup"><span data-stu-id="0a5f2-119">To use this SAP HANA connector, you need to:</span></span>

- <span data-ttu-id="0a5f2-120">Set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-120">Set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="0a5f2-121">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-121">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span></span>
- <span data-ttu-id="0a5f2-122">Install the SAP HANA ODBC driver on the Integration Runtime machine.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-122">Install the SAP HANA ODBC driver on the Integration Runtime machine.</span></span> <span data-ttu-id="0a5f2-123">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="0a5f2-123">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="0a5f2-124">Search with the keyword **SAP HANA CLIENT for Windows**.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-124">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0a5f2-125">Getting started</span><span class="sxs-lookup"><span data-stu-id="0a5f2-125">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="0a5f2-126">The following sections provide details about properties that are used to define Data Factory entities specific to SAP HANA connector.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-126">The following sections provide details about properties that are used to define Data Factory entities specific to SAP HANA connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0a5f2-127">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="0a5f2-127">Linked service properties</span></span>

<span data-ttu-id="0a5f2-128">The following properties are supported for SAP HANA linked service:</span><span class="sxs-lookup"><span data-stu-id="0a5f2-128">The following properties are supported for SAP HANA linked service:</span></span>

| <span data-ttu-id="0a5f2-129">Property</span><span class="sxs-lookup"><span data-stu-id="0a5f2-129">Property</span></span> | <span data-ttu-id="0a5f2-130">Description</span><span class="sxs-lookup"><span data-stu-id="0a5f2-130">Description</span></span> | <span data-ttu-id="0a5f2-131">Required</span><span class="sxs-lookup"><span data-stu-id="0a5f2-131">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0a5f2-132">type</span><span class="sxs-lookup"><span data-stu-id="0a5f2-132">type</span></span> | <span data-ttu-id="0a5f2-133">The type property must be set to: **SapHana**</span><span class="sxs-lookup"><span data-stu-id="0a5f2-133">The type property must be set to: **SapHana**</span></span> | <span data-ttu-id="0a5f2-134">Yes</span><span class="sxs-lookup"><span data-stu-id="0a5f2-134">Yes</span></span> |
| <span data-ttu-id="0a5f2-135">server</span><span class="sxs-lookup"><span data-stu-id="0a5f2-135">server</span></span> | <span data-ttu-id="0a5f2-136">Name of the server on which the SAP HANA instance resides.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-136">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="0a5f2-137">If your server is using a customized port, specify `server:port`.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-137">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="0a5f2-138">Yes</span><span class="sxs-lookup"><span data-stu-id="0a5f2-138">Yes</span></span> |
| <span data-ttu-id="0a5f2-139">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0a5f2-139">authenticationType</span></span> | <span data-ttu-id="0a5f2-140">Type of authentication used to connect to the SAP HANA database.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-140">Type of authentication used to connect to the SAP HANA database.</span></span><br/><span data-ttu-id="0a5f2-141">Allowed values are: **Basic**, and **Windows**</span><span class="sxs-lookup"><span data-stu-id="0a5f2-141">Allowed values are: **Basic**, and **Windows**</span></span> | <span data-ttu-id="0a5f2-142">Yes</span><span class="sxs-lookup"><span data-stu-id="0a5f2-142">Yes</span></span> |
| <span data-ttu-id="0a5f2-143">userName</span><span class="sxs-lookup"><span data-stu-id="0a5f2-143">userName</span></span> | <span data-ttu-id="0a5f2-144">Name of the user who has access to the SAP server.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-144">Name of the user who has access to the SAP server.</span></span> | <span data-ttu-id="0a5f2-145">Yes</span><span class="sxs-lookup"><span data-stu-id="0a5f2-145">Yes</span></span> |
| <span data-ttu-id="0a5f2-146">password</span><span class="sxs-lookup"><span data-stu-id="0a5f2-146">password</span></span> | <span data-ttu-id="0a5f2-147">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-147">Password for the user.</span></span> <span data-ttu-id="0a5f2-148">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="0a5f2-148">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="0a5f2-149">Yes</span><span class="sxs-lookup"><span data-stu-id="0a5f2-149">Yes</span></span> |
| <span data-ttu-id="0a5f2-150">connectVia</span><span class="sxs-lookup"><span data-stu-id="0a5f2-150">connectVia</span></span> | <span data-ttu-id="0a5f2-151">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-151">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="0a5f2-152">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="0a5f2-152">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span></span> |<span data-ttu-id="0a5f2-153">Yes</span><span class="sxs-lookup"><span data-stu-id="0a5f2-153">Yes</span></span> |

<span data-ttu-id="0a5f2-154">**Example:**</span><span class="sxs-lookup"><span data-stu-id="0a5f2-154">**Example:**</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server>:<port (optional)>",
            "authenticationType": "Basic",
            "userName": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="0a5f2-155">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="0a5f2-155">Dataset properties</span></span>

<span data-ttu-id="0a5f2-156">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-156">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="0a5f2-157">This section provides a list of properties supported by SAP HANA dataset.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-157">This section provides a list of properties supported by SAP HANA dataset.</span></span>

<span data-ttu-id="0a5f2-158">To copy data from SAP HANA, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-158">To copy data from SAP HANA, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="0a5f2-159">While there are no type-specific properties supported for the SAP HANA dataset of type RelationalTable.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-159">While there are no type-specific properties supported for the SAP HANA dataset of type RelationalTable.</span></span>

<span data-ttu-id="0a5f2-160">**Example:**</span><span class="sxs-lookup"><span data-stu-id="0a5f2-160">**Example:**</span></span>

```json
{
    "name": "SAPHANADataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<SAP HANA linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="0a5f2-161">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="0a5f2-161">Copy activity properties</span></span>

<span data-ttu-id="0a5f2-162">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-162">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="0a5f2-163">This section provides a list of properties supported by SAP HANA source.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-163">This section provides a list of properties supported by SAP HANA source.</span></span>

### <a name="sap-hana-as-source"></a><span data-ttu-id="0a5f2-164">SAP HANA as source</span><span class="sxs-lookup"><span data-stu-id="0a5f2-164">SAP HANA as source</span></span>

<span data-ttu-id="0a5f2-165">To copy data from SAP HANA, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-165">To copy data from SAP HANA, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="0a5f2-166">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="0a5f2-166">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="0a5f2-167">Property</span><span class="sxs-lookup"><span data-stu-id="0a5f2-167">Property</span></span> | <span data-ttu-id="0a5f2-168">Description</span><span class="sxs-lookup"><span data-stu-id="0a5f2-168">Description</span></span> | <span data-ttu-id="0a5f2-169">Required</span><span class="sxs-lookup"><span data-stu-id="0a5f2-169">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0a5f2-170">type</span><span class="sxs-lookup"><span data-stu-id="0a5f2-170">type</span></span> | <span data-ttu-id="0a5f2-171">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="0a5f2-171">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="0a5f2-172">Yes</span><span class="sxs-lookup"><span data-stu-id="0a5f2-172">Yes</span></span> |
| <span data-ttu-id="0a5f2-173">query</span><span class="sxs-lookup"><span data-stu-id="0a5f2-173">query</span></span> | <span data-ttu-id="0a5f2-174">Specifies the SQL query to read data from the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-174">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="0a5f2-175">Yes</span><span class="sxs-lookup"><span data-stu-id="0a5f2-175">Yes</span></span> |

<span data-ttu-id="0a5f2-176">**Example:**</span><span class="sxs-lookup"><span data-stu-id="0a5f2-176">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSAPHANA",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SAP HANA input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "RelationalSource",
                "query": "<SQL query for SAP HANA>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-sap-hana"></a><span data-ttu-id="0a5f2-177">Data type mapping for SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0a5f2-177">Data type mapping for SAP HANA</span></span>

<span data-ttu-id="0a5f2-178">When copying data from SAP HANA, the following mappings are used from SAP HANA data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-178">When copying data from SAP HANA, the following mappings are used from SAP HANA data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="0a5f2-179">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="0a5f2-179">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="0a5f2-180">SAP HANA data type</span><span class="sxs-lookup"><span data-stu-id="0a5f2-180">SAP HANA data type</span></span> | <span data-ttu-id="0a5f2-181">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="0a5f2-181">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="0a5f2-182">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="0a5f2-182">ALPHANUM</span></span> | <span data-ttu-id="0a5f2-183">String</span><span class="sxs-lookup"><span data-stu-id="0a5f2-183">String</span></span> |
| <span data-ttu-id="0a5f2-184">BIGINT</span><span class="sxs-lookup"><span data-stu-id="0a5f2-184">BIGINT</span></span> | <span data-ttu-id="0a5f2-185">Int64</span><span class="sxs-lookup"><span data-stu-id="0a5f2-185">Int64</span></span> |
| <span data-ttu-id="0a5f2-186">BLOB</span><span class="sxs-lookup"><span data-stu-id="0a5f2-186">BLOB</span></span> | <span data-ttu-id="0a5f2-187">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0a5f2-187">Byte[]</span></span> |
| <span data-ttu-id="0a5f2-188">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="0a5f2-188">BOOLEAN</span></span> | <span data-ttu-id="0a5f2-189">Byte</span><span class="sxs-lookup"><span data-stu-id="0a5f2-189">Byte</span></span> |
| <span data-ttu-id="0a5f2-190">CLOB</span><span class="sxs-lookup"><span data-stu-id="0a5f2-190">CLOB</span></span> | <span data-ttu-id="0a5f2-191">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0a5f2-191">Byte[]</span></span> |
| <span data-ttu-id="0a5f2-192">DATE</span><span class="sxs-lookup"><span data-stu-id="0a5f2-192">DATE</span></span> | <span data-ttu-id="0a5f2-193">DateTime</span><span class="sxs-lookup"><span data-stu-id="0a5f2-193">DateTime</span></span> |
| <span data-ttu-id="0a5f2-194">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="0a5f2-194">DECIMAL</span></span> | <span data-ttu-id="0a5f2-195">Decimal</span><span class="sxs-lookup"><span data-stu-id="0a5f2-195">Decimal</span></span> |
| <span data-ttu-id="0a5f2-196">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="0a5f2-196">DOUBLE</span></span> | <span data-ttu-id="0a5f2-197">Single</span><span class="sxs-lookup"><span data-stu-id="0a5f2-197">Single</span></span> |
| <span data-ttu-id="0a5f2-198">INT</span><span class="sxs-lookup"><span data-stu-id="0a5f2-198">INT</span></span> | <span data-ttu-id="0a5f2-199">Int32</span><span class="sxs-lookup"><span data-stu-id="0a5f2-199">Int32</span></span> |
| <span data-ttu-id="0a5f2-200">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="0a5f2-200">NVARCHAR</span></span> | <span data-ttu-id="0a5f2-201">String</span><span class="sxs-lookup"><span data-stu-id="0a5f2-201">String</span></span> |
| <span data-ttu-id="0a5f2-202">REAL</span><span class="sxs-lookup"><span data-stu-id="0a5f2-202">REAL</span></span> | <span data-ttu-id="0a5f2-203">Single</span><span class="sxs-lookup"><span data-stu-id="0a5f2-203">Single</span></span> |
| <span data-ttu-id="0a5f2-204">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="0a5f2-204">SECONDDATE</span></span> | <span data-ttu-id="0a5f2-205">DateTime</span><span class="sxs-lookup"><span data-stu-id="0a5f2-205">DateTime</span></span> |
| <span data-ttu-id="0a5f2-206">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="0a5f2-206">SMALLINT</span></span> | <span data-ttu-id="0a5f2-207">Int16</span><span class="sxs-lookup"><span data-stu-id="0a5f2-207">Int16</span></span> |
| <span data-ttu-id="0a5f2-208">TIME</span><span class="sxs-lookup"><span data-stu-id="0a5f2-208">TIME</span></span> | <span data-ttu-id="0a5f2-209">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0a5f2-209">TimeSpan</span></span> |
| <span data-ttu-id="0a5f2-210">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="0a5f2-210">TIMESTAMP</span></span> | <span data-ttu-id="0a5f2-211">DateTime</span><span class="sxs-lookup"><span data-stu-id="0a5f2-211">DateTime</span></span> |
| <span data-ttu-id="0a5f2-212">TINYINT</span><span class="sxs-lookup"><span data-stu-id="0a5f2-212">TINYINT</span></span> | <span data-ttu-id="0a5f2-213">Byte</span><span class="sxs-lookup"><span data-stu-id="0a5f2-213">Byte</span></span> |
| <span data-ttu-id="0a5f2-214">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="0a5f2-214">VARCHAR</span></span> | <span data-ttu-id="0a5f2-215">String</span><span class="sxs-lookup"><span data-stu-id="0a5f2-215">String</span></span> |

## <a name="known-limitations"></a><span data-ttu-id="0a5f2-216">Known limitations</span><span class="sxs-lookup"><span data-stu-id="0a5f2-216">Known limitations</span></span>

<span data-ttu-id="0a5f2-217">There are a few known limitations when copying data from SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="0a5f2-217">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="0a5f2-218">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span><span class="sxs-lookup"><span data-stu-id="0a5f2-218">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="0a5f2-219">SMALLDECIMAL is not supported</span><span class="sxs-lookup"><span data-stu-id="0a5f2-219">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="0a5f2-220">VARBINARY is not supported</span><span class="sxs-lookup"><span data-stu-id="0a5f2-220">VARBINARY is not supported</span></span>
- <span data-ttu-id="0a5f2-221">Valid Dates are between 1899/12/30 and 9999/12/31</span><span class="sxs-lookup"><span data-stu-id="0a5f2-221">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>


## <a name="next-steps"></a><span data-ttu-id="0a5f2-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a5f2-222">Next steps</span></span>
<span data-ttu-id="0a5f2-223">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0a5f2-223">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
