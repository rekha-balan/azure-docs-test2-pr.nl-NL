---
title: Copy data from ODBC sources using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from OData sources to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 26a1448ddf3f7ffb08ab581b1dad1abfd3ca8e12
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857238"
---
# <a name="copy-data-from-and-to-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="14fd7-103">Copy data from and to ODBC data stores using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="14fd7-103">Copy data from and to ODBC data stores using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-odbc-connector.md)
> * [Current version](connector-odbc.md)

<span data-ttu-id="14fd7-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from and to an ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from and to an ODBC data store.</span></span> <span data-ttu-id="14fd7-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="14fd7-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="14fd7-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="14fd7-108">Supported capabilities</span></span>

<span data-ttu-id="14fd7-109">You can copy data from ODBC source to any supported sink data store, or copy from any supported source data store to ODBC sink.</span><span class="sxs-lookup"><span data-stu-id="14fd7-109">You can copy data from ODBC source to any supported sink data store, or copy from any supported source data store to ODBC sink.</span></span> <span data-ttu-id="14fd7-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="14fd7-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="14fd7-111">Specifically, this ODBC connector supports copying data from/to **any ODBC-compatible data stores** using **Basic** or **Anonymous** authentication.</span><span class="sxs-lookup"><span data-stu-id="14fd7-111">Specifically, this ODBC connector supports copying data from/to **any ODBC-compatible data stores** using **Basic** or **Anonymous** authentication.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14fd7-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="14fd7-112">Prerequisites</span></span>

<span data-ttu-id="14fd7-113">To use this ODBC connector, you need to:</span><span class="sxs-lookup"><span data-stu-id="14fd7-113">To use this ODBC connector, you need to:</span></span>

- <span data-ttu-id="14fd7-114">Set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="14fd7-114">Set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="14fd7-115">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="14fd7-115">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span></span>
- <span data-ttu-id="14fd7-116">Install the ODBC driver for the data store on the Integration Runtime machine.</span><span class="sxs-lookup"><span data-stu-id="14fd7-116">Install the ODBC driver for the data store on the Integration Runtime machine.</span></span>

## <a name="getting-started"></a><span data-ttu-id="14fd7-117">Getting started</span><span class="sxs-lookup"><span data-stu-id="14fd7-117">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="14fd7-118">The following sections provide details about properties that are used to define Data Factory entities specific to ODBC connector.</span><span class="sxs-lookup"><span data-stu-id="14fd7-118">The following sections provide details about properties that are used to define Data Factory entities specific to ODBC connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="14fd7-119">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="14fd7-119">Linked service properties</span></span>

<span data-ttu-id="14fd7-120">The following properties are supported for ODBC linked service:</span><span class="sxs-lookup"><span data-stu-id="14fd7-120">The following properties are supported for ODBC linked service:</span></span>

| <span data-ttu-id="14fd7-121">Property</span><span class="sxs-lookup"><span data-stu-id="14fd7-121">Property</span></span> | <span data-ttu-id="14fd7-122">Description</span><span class="sxs-lookup"><span data-stu-id="14fd7-122">Description</span></span> | <span data-ttu-id="14fd7-123">Required</span><span class="sxs-lookup"><span data-stu-id="14fd7-123">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="14fd7-124">type</span><span class="sxs-lookup"><span data-stu-id="14fd7-124">type</span></span> | <span data-ttu-id="14fd7-125">The type property must be set to: **Odbc**</span><span class="sxs-lookup"><span data-stu-id="14fd7-125">The type property must be set to: **Odbc**</span></span> | <span data-ttu-id="14fd7-126">Yes</span><span class="sxs-lookup"><span data-stu-id="14fd7-126">Yes</span></span> |
| <span data-ttu-id="14fd7-127">connectionString</span><span class="sxs-lookup"><span data-stu-id="14fd7-127">connectionString</span></span> | <span data-ttu-id="14fd7-128">The connection string excluding the credential portion.</span><span class="sxs-lookup"><span data-stu-id="14fd7-128">The connection string excluding the credential portion.</span></span> <span data-ttu-id="14fd7-129">You can specify the connection string with pattern like `"Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;"`, or use the system DSN (Data Source Name) you set up on the Integration Runtime machine with `"DSN=<name of the DSN on IR machine>;"` (you need still specify the credential portion in linked service accordingly).</span><span class="sxs-lookup"><span data-stu-id="14fd7-129">You can specify the connection string with pattern like `"Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;"`, or use the system DSN (Data Source Name) you set up on the Integration Runtime machine with `"DSN=<name of the DSN on IR machine>;"` (you need still specify the credential portion in linked service accordingly).</span></span><br><span data-ttu-id="14fd7-130">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="14fd7-130">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span>| <span data-ttu-id="14fd7-131">Yes</span><span class="sxs-lookup"><span data-stu-id="14fd7-131">Yes</span></span> |
| <span data-ttu-id="14fd7-132">authenticationType</span><span class="sxs-lookup"><span data-stu-id="14fd7-132">authenticationType</span></span> | <span data-ttu-id="14fd7-133">Type of authentication used to connect to the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-133">Type of authentication used to connect to the ODBC data store.</span></span><br/><span data-ttu-id="14fd7-134">Allowed values are: **Basic** and **Anonymous**.</span><span class="sxs-lookup"><span data-stu-id="14fd7-134">Allowed values are: **Basic** and **Anonymous**.</span></span> | <span data-ttu-id="14fd7-135">Yes</span><span class="sxs-lookup"><span data-stu-id="14fd7-135">Yes</span></span> |
| <span data-ttu-id="14fd7-136">userName</span><span class="sxs-lookup"><span data-stu-id="14fd7-136">userName</span></span> | <span data-ttu-id="14fd7-137">Specify user name if you are using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="14fd7-137">Specify user name if you are using Basic authentication.</span></span> | <span data-ttu-id="14fd7-138">No</span><span class="sxs-lookup"><span data-stu-id="14fd7-138">No</span></span> |
| <span data-ttu-id="14fd7-139">password</span><span class="sxs-lookup"><span data-stu-id="14fd7-139">password</span></span> | <span data-ttu-id="14fd7-140">Specify password for the user account you specified for the userName.</span><span class="sxs-lookup"><span data-stu-id="14fd7-140">Specify password for the user account you specified for the userName.</span></span> <span data-ttu-id="14fd7-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="14fd7-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="14fd7-142">No</span><span class="sxs-lookup"><span data-stu-id="14fd7-142">No</span></span> |
| <span data-ttu-id="14fd7-143">credential</span><span class="sxs-lookup"><span data-stu-id="14fd7-143">credential</span></span> | <span data-ttu-id="14fd7-144">The access credential portion of the connection string specified in driver-specific property-value format.</span><span class="sxs-lookup"><span data-stu-id="14fd7-144">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="14fd7-145">Example: `"RefreshToken=<secret refresh token>;"`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-145">Example: `"RefreshToken=<secret refresh token>;"`.</span></span> <span data-ttu-id="14fd7-146">Mark this field as a SecureString.</span><span class="sxs-lookup"><span data-stu-id="14fd7-146">Mark this field as a SecureString.</span></span> | <span data-ttu-id="14fd7-147">No</span><span class="sxs-lookup"><span data-stu-id="14fd7-147">No</span></span> |
| <span data-ttu-id="14fd7-148">connectVia</span><span class="sxs-lookup"><span data-stu-id="14fd7-148">connectVia</span></span> | <span data-ttu-id="14fd7-149">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-149">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="14fd7-150">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="14fd7-150">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span></span> |<span data-ttu-id="14fd7-151">Yes</span><span class="sxs-lookup"><span data-stu-id="14fd7-151">Yes</span></span> |

<span data-ttu-id="14fd7-152">**Example 1: using Basic authentication**</span><span class="sxs-lookup"><span data-stu-id="14fd7-152">**Example 1: using Basic authentication**</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "Odbc",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "<connection string>"
            },
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

<span data-ttu-id="14fd7-153">**Example 2: using Anonymous authentication**</span><span class="sxs-lookup"><span data-stu-id="14fd7-153">**Example 2: using Anonymous authentication**</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "Odbc",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "<connection string>"
            },
            "authenticationType": "Anonymous",
            "credential": {
                "type": "SecureString",
                "value": "RefreshToken=<secret refresh token>;"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="14fd7-154">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="14fd7-154">Dataset properties</span></span>

<span data-ttu-id="14fd7-155">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="14fd7-155">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="14fd7-156">This section provides a list of properties supported by ODBC dataset.</span><span class="sxs-lookup"><span data-stu-id="14fd7-156">This section provides a list of properties supported by ODBC dataset.</span></span>

<span data-ttu-id="14fd7-157">To copy data from/to ODBC-compatible data store, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="14fd7-157">To copy data from/to ODBC-compatible data store, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="14fd7-158">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="14fd7-158">The following properties are supported:</span></span>

| <span data-ttu-id="14fd7-159">Property</span><span class="sxs-lookup"><span data-stu-id="14fd7-159">Property</span></span> | <span data-ttu-id="14fd7-160">Description</span><span class="sxs-lookup"><span data-stu-id="14fd7-160">Description</span></span> | <span data-ttu-id="14fd7-161">Required</span><span class="sxs-lookup"><span data-stu-id="14fd7-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="14fd7-162">type</span><span class="sxs-lookup"><span data-stu-id="14fd7-162">type</span></span> | <span data-ttu-id="14fd7-163">The type property of the dataset must be set to: **RelationalTable**</span><span class="sxs-lookup"><span data-stu-id="14fd7-163">The type property of the dataset must be set to: **RelationalTable**</span></span> | <span data-ttu-id="14fd7-164">Yes</span><span class="sxs-lookup"><span data-stu-id="14fd7-164">Yes</span></span> |
| <span data-ttu-id="14fd7-165">tableName</span><span class="sxs-lookup"><span data-stu-id="14fd7-165">tableName</span></span> | <span data-ttu-id="14fd7-166">Name of the table in the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-166">Name of the table in the ODBC data store.</span></span> | <span data-ttu-id="14fd7-167">No for source (if "query" in activity source is specified);</span><span class="sxs-lookup"><span data-stu-id="14fd7-167">No for source (if "query" in activity source is specified);</span></span><br/><span data-ttu-id="14fd7-168">Yes for sink</span><span class="sxs-lookup"><span data-stu-id="14fd7-168">Yes for sink</span></span> |

<span data-ttu-id="14fd7-169">**Example**</span><span class="sxs-lookup"><span data-stu-id="14fd7-169">**Example**</span></span>

```json
{
    "name": "ODBCDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<ODBC linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "<table name>"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="14fd7-170">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="14fd7-170">Copy activity properties</span></span>

<span data-ttu-id="14fd7-171">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="14fd7-171">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="14fd7-172">This section provides a list of properties supported by ODBC source.</span><span class="sxs-lookup"><span data-stu-id="14fd7-172">This section provides a list of properties supported by ODBC source.</span></span>

### <a name="odbc-as-source"></a><span data-ttu-id="14fd7-173">ODBC as source</span><span class="sxs-lookup"><span data-stu-id="14fd7-173">ODBC as source</span></span>

<span data-ttu-id="14fd7-174">To copy data from ODBC-compatible data store, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="14fd7-174">To copy data from ODBC-compatible data store, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="14fd7-175">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="14fd7-175">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="14fd7-176">Property</span><span class="sxs-lookup"><span data-stu-id="14fd7-176">Property</span></span> | <span data-ttu-id="14fd7-177">Description</span><span class="sxs-lookup"><span data-stu-id="14fd7-177">Description</span></span> | <span data-ttu-id="14fd7-178">Required</span><span class="sxs-lookup"><span data-stu-id="14fd7-178">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="14fd7-179">type</span><span class="sxs-lookup"><span data-stu-id="14fd7-179">type</span></span> | <span data-ttu-id="14fd7-180">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="14fd7-180">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="14fd7-181">Yes</span><span class="sxs-lookup"><span data-stu-id="14fd7-181">Yes</span></span> |
| <span data-ttu-id="14fd7-182">query</span><span class="sxs-lookup"><span data-stu-id="14fd7-182">query</span></span> | <span data-ttu-id="14fd7-183">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="14fd7-183">Use the custom SQL query to read data.</span></span> <span data-ttu-id="14fd7-184">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-184">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="14fd7-185">No (if "tableName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="14fd7-185">No (if "tableName" in dataset is specified)</span></span> |

<span data-ttu-id="14fd7-186">**Example:**</span><span class="sxs-lookup"><span data-stu-id="14fd7-186">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromODBC",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<ODBC input dataset name>",
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
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="odbc-as-sink"></a><span data-ttu-id="14fd7-187">ODBC as sink</span><span class="sxs-lookup"><span data-stu-id="14fd7-187">ODBC as sink</span></span>

<span data-ttu-id="14fd7-188">To copy data to ODBC-compatible data store, set the sink type in the copy activity to **OdbcSink**.</span><span class="sxs-lookup"><span data-stu-id="14fd7-188">To copy data to ODBC-compatible data store, set the sink type in the copy activity to **OdbcSink**.</span></span> <span data-ttu-id="14fd7-189">The following properties are supported in the copy activity **sink** section:</span><span class="sxs-lookup"><span data-stu-id="14fd7-189">The following properties are supported in the copy activity **sink** section:</span></span>

| <span data-ttu-id="14fd7-190">Property</span><span class="sxs-lookup"><span data-stu-id="14fd7-190">Property</span></span> | <span data-ttu-id="14fd7-191">Description</span><span class="sxs-lookup"><span data-stu-id="14fd7-191">Description</span></span> | <span data-ttu-id="14fd7-192">Required</span><span class="sxs-lookup"><span data-stu-id="14fd7-192">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="14fd7-193">type</span><span class="sxs-lookup"><span data-stu-id="14fd7-193">type</span></span> | <span data-ttu-id="14fd7-194">The type property of the copy activity sink must be set to: **OdbcSink**</span><span class="sxs-lookup"><span data-stu-id="14fd7-194">The type property of the copy activity sink must be set to: **OdbcSink**</span></span> | <span data-ttu-id="14fd7-195">Yes</span><span class="sxs-lookup"><span data-stu-id="14fd7-195">Yes</span></span> |
| <span data-ttu-id="14fd7-196">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="14fd7-196">writeBatchTimeout</span></span> |<span data-ttu-id="14fd7-197">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="14fd7-197">Wait time for the batch insert operation to complete before it times out.</span></span><br/><span data-ttu-id="14fd7-198">Allowed values are: timespan.</span><span class="sxs-lookup"><span data-stu-id="14fd7-198">Allowed values are: timespan.</span></span> <span data-ttu-id="14fd7-199">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="14fd7-199">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="14fd7-200">No</span><span class="sxs-lookup"><span data-stu-id="14fd7-200">No</span></span> |
| <span data-ttu-id="14fd7-201">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="14fd7-201">writeBatchSize</span></span> |<span data-ttu-id="14fd7-202">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="14fd7-202">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span><br/><span data-ttu-id="14fd7-203">Allowed values are: integer (number of rows).</span><span class="sxs-lookup"><span data-stu-id="14fd7-203">Allowed values are: integer (number of rows).</span></span> |<span data-ttu-id="14fd7-204">No (default is 0 - auto detected)</span><span class="sxs-lookup"><span data-stu-id="14fd7-204">No (default is 0 - auto detected)</span></span> |
| <span data-ttu-id="14fd7-205">preCopyScript</span><span class="sxs-lookup"><span data-stu-id="14fd7-205">preCopyScript</span></span> |<span data-ttu-id="14fd7-206">Specify a SQL query for Copy Activity to execute before writing data into data store in each run.</span><span class="sxs-lookup"><span data-stu-id="14fd7-206">Specify a SQL query for Copy Activity to execute before writing data into data store in each run.</span></span> <span data-ttu-id="14fd7-207">You can use this property to clean up the pre-loaded data.</span><span class="sxs-lookup"><span data-stu-id="14fd7-207">You can use this property to clean up the pre-loaded data.</span></span> |<span data-ttu-id="14fd7-208">No</span><span class="sxs-lookup"><span data-stu-id="14fd7-208">No</span></span> |

> [!NOTE]
> For "writeBatchSize", if it's not set (auto-detected), copy activity first detects whether the driver supports batch operations, and set it to 10000 if it does, or set it to 1 if it doesn’t. If you explicitly set the value other than 0, copy activity honors the value and fails at runtime if the driver doesn’t support batch operations.

<span data-ttu-id="14fd7-211">**Example:**</span><span class="sxs-lookup"><span data-stu-id="14fd7-211">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyToODBC",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<ODBC output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "OdbcSink",
                "writeBatchSize": 100000
            }
        }
    }
]
```

## <a name="ibm-informix-source"></a><span data-ttu-id="14fd7-212">IBM Informix source</span><span class="sxs-lookup"><span data-stu-id="14fd7-212">IBM Informix source</span></span>

<span data-ttu-id="14fd7-213">You can copy data from IBM Informix database using the generic ODBC connector.</span><span class="sxs-lookup"><span data-stu-id="14fd7-213">You can copy data from IBM Informix database using the generic ODBC connector.</span></span>

<span data-ttu-id="14fd7-214">Set up a Self-hosted Integration Runtime on a machine with access to your data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-214">Set up a Self-hosted Integration Runtime on a machine with access to your data store.</span></span> <span data-ttu-id="14fd7-215">The Integration Runtime uses the ODBC driver for Informix to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-215">The Integration Runtime uses the ODBC driver for Informix to connect to the data store.</span></span> <span data-ttu-id="14fd7-216">Therefore, install the driver if it is not already installed on the same machine.</span><span class="sxs-lookup"><span data-stu-id="14fd7-216">Therefore, install the driver if it is not already installed on the same machine.</span></span> <span data-ttu-id="14fd7-217">For example, you can use driver "IBM INFORMIX ODBC DRIVER (64-bit)".</span><span class="sxs-lookup"><span data-stu-id="14fd7-217">For example, you can use driver "IBM INFORMIX ODBC DRIVER (64-bit)".</span></span> <span data-ttu-id="14fd7-218">See [Prerequisites](#prerequisites) section for details.</span><span class="sxs-lookup"><span data-stu-id="14fd7-218">See [Prerequisites](#prerequisites) section for details.</span></span>

<span data-ttu-id="14fd7-219">Before you use the Informix source in a Data Factory solution, verify whether the Integration Runtime can connect to the data store using instructions in [Troubleshoot connectivity issues](#troubleshoot-connectivity-issues) section.</span><span class="sxs-lookup"><span data-stu-id="14fd7-219">Before you use the Informix source in a Data Factory solution, verify whether the Integration Runtime can connect to the data store using instructions in [Troubleshoot connectivity issues](#troubleshoot-connectivity-issues) section.</span></span>

<span data-ttu-id="14fd7-220">Create an ODBC linked service to link a IBM Informix data store to an Azure data factory as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="14fd7-220">Create an ODBC linked service to link a IBM Informix data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "InformixLinkedService",
    "properties": {
        "type": "Odbc",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "<Informix connection string or DSN>"
            },
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

<span data-ttu-id="14fd7-221">Read the article from the beginning for a detailed overview of using ODBC data stores as source/sink data stores in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="14fd7-221">Read the article from the beginning for a detailed overview of using ODBC data stores as source/sink data stores in a copy operation.</span></span>

## <a name="microsoft-access-source"></a><span data-ttu-id="14fd7-222">Microsoft Access source</span><span class="sxs-lookup"><span data-stu-id="14fd7-222">Microsoft Access source</span></span>

<span data-ttu-id="14fd7-223">You can copy data from Microsoft Access database using the generic ODBC connector.</span><span class="sxs-lookup"><span data-stu-id="14fd7-223">You can copy data from Microsoft Access database using the generic ODBC connector.</span></span>

<span data-ttu-id="14fd7-224">Set up a Self-hosted Integration Runtime on a machine with access to your data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-224">Set up a Self-hosted Integration Runtime on a machine with access to your data store.</span></span> <span data-ttu-id="14fd7-225">The Integration Runtime uses the ODBC driver for Microsoft Access to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-225">The Integration Runtime uses the ODBC driver for Microsoft Access to connect to the data store.</span></span> <span data-ttu-id="14fd7-226">Therefore, install the driver if it is not already installed on the same machine.</span><span class="sxs-lookup"><span data-stu-id="14fd7-226">Therefore, install the driver if it is not already installed on the same machine.</span></span> <span data-ttu-id="14fd7-227">See [Prerequisites](#prerequisites) section for details.</span><span class="sxs-lookup"><span data-stu-id="14fd7-227">See [Prerequisites](#prerequisites) section for details.</span></span>

<span data-ttu-id="14fd7-228">Before you use the Microsoft Access source in a Data Factory solution, verify whether the Integration Runtime can connect to the data store using instructions in [Troubleshoot connectivity issues](#troubleshoot-connectivity-issues) section.</span><span class="sxs-lookup"><span data-stu-id="14fd7-228">Before you use the Microsoft Access source in a Data Factory solution, verify whether the Integration Runtime can connect to the data store using instructions in [Troubleshoot connectivity issues](#troubleshoot-connectivity-issues) section.</span></span>

<span data-ttu-id="14fd7-229">Create an ODBC linked service to link a Microsoft Access database to an Azure data factory as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="14fd7-229">Create an ODBC linked service to link a Microsoft Access database to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "MicrosoftAccessLinkedService",
    "properties": {
        "type": "Odbc",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Driver={Microsoft Access Driver (*.mdb, *.accdb)};Dbq=<path to your DB file e.g. C:\\mydatabase.accdb>;"
            },
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

<span data-ttu-id="14fd7-230">Read the article from the beginning for a detailed overview of using ODBC data stores as source/sink data stores in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="14fd7-230">Read the article from the beginning for a detailed overview of using ODBC data stores as source/sink data stores in a copy operation.</span></span>

## <a name="ge-historian-source"></a><span data-ttu-id="14fd7-231">GE Historian source</span><span class="sxs-lookup"><span data-stu-id="14fd7-231">GE Historian source</span></span>

<span data-ttu-id="14fd7-232">You can copy data from GE Historian using the generic ODBC connector.</span><span class="sxs-lookup"><span data-stu-id="14fd7-232">You can copy data from GE Historian using the generic ODBC connector.</span></span>

<span data-ttu-id="14fd7-233">Set up a Self-hosted Integration Runtime on a machine with access to your data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-233">Set up a Self-hosted Integration Runtime on a machine with access to your data store.</span></span> <span data-ttu-id="14fd7-234">The Integration Runtime uses the ODBC driver for GE Historian to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-234">The Integration Runtime uses the ODBC driver for GE Historian to connect to the data store.</span></span> <span data-ttu-id="14fd7-235">Therefore, install the driver if it is not already installed on the same machine.</span><span class="sxs-lookup"><span data-stu-id="14fd7-235">Therefore, install the driver if it is not already installed on the same machine.</span></span> <span data-ttu-id="14fd7-236">See [Prerequisites](#prerequisites) section for details.</span><span class="sxs-lookup"><span data-stu-id="14fd7-236">See [Prerequisites](#prerequisites) section for details.</span></span>

<span data-ttu-id="14fd7-237">Before you use the GE Historian source in a Data Factory solution, verify whether the Integration Runtime can connect to the data store using instructions in [Troubleshoot connectivity issues](#troubleshoot-connectivity-issues) section.</span><span class="sxs-lookup"><span data-stu-id="14fd7-237">Before you use the GE Historian source in a Data Factory solution, verify whether the Integration Runtime can connect to the data store using instructions in [Troubleshoot connectivity issues](#troubleshoot-connectivity-issues) section.</span></span>

<span data-ttu-id="14fd7-238">Create an ODBC linked service to link a Microsoft Access database to an Azure data factory as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="14fd7-238">Create an ODBC linked service to link a Microsoft Access database to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties": {
        "type": "Odbc",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "<GE Historian store connection string or DSN>"
            },
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

<span data-ttu-id="14fd7-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source/sink data stores in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="14fd7-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source/sink data stores in a copy operation.</span></span>

## <a name="sap-hana-sink"></a><span data-ttu-id="14fd7-240">SAP HANA sink</span><span class="sxs-lookup"><span data-stu-id="14fd7-240">SAP HANA sink</span></span>

>[!NOTE]
>To copy data from SAP HANA data store, refer to native [SAP HANA connector](connector-sap-hana.md). To copy data to SAP HANA, please follow this instruction to use ODBC connector. Note the linked services for SAP HANA connector and ODBC connector are with different type thus cannot be reused.
>

<span data-ttu-id="14fd7-244">You can copy data to SAP HANA database using the generic ODBC connector.</span><span class="sxs-lookup"><span data-stu-id="14fd7-244">You can copy data to SAP HANA database using the generic ODBC connector.</span></span>

<span data-ttu-id="14fd7-245">Set up a Self-hosted Integration Runtime on a machine with access to your data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-245">Set up a Self-hosted Integration Runtime on a machine with access to your data store.</span></span> <span data-ttu-id="14fd7-246">The Integration Runtime uses the ODBC driver for SAP HANA to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-246">The Integration Runtime uses the ODBC driver for SAP HANA to connect to the data store.</span></span> <span data-ttu-id="14fd7-247">Therefore, install the driver if it is not already installed on the same machine.</span><span class="sxs-lookup"><span data-stu-id="14fd7-247">Therefore, install the driver if it is not already installed on the same machine.</span></span> <span data-ttu-id="14fd7-248">See [Prerequisites](#prerequisites) section for details.</span><span class="sxs-lookup"><span data-stu-id="14fd7-248">See [Prerequisites](#prerequisites) section for details.</span></span>

<span data-ttu-id="14fd7-249">Before you use the SAP HANA sink in a Data Factory solution, verify whether the Integration Runtime can connect to the data store using instructions in [Troubleshoot connectivity issues](#troubleshoot-connectivity-issues) section.</span><span class="sxs-lookup"><span data-stu-id="14fd7-249">Before you use the SAP HANA sink in a Data Factory solution, verify whether the Integration Runtime can connect to the data store using instructions in [Troubleshoot connectivity issues](#troubleshoot-connectivity-issues) section.</span></span>

<span data-ttu-id="14fd7-250">Create an ODBC linked service to link a SAP HANA data store to an Azure data factory as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="14fd7-250">Create an ODBC linked service to link a SAP HANA data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "SAPHANAViaODBCLinkedService",
    "properties": {
        "type": "Odbc",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Driver={HDBODBC};servernode=<HANA server>.clouddatahub-int.net:30015"
            },
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

<span data-ttu-id="14fd7-251">Read the article from the beginning for a detailed overview of using ODBC data stores as source/sink data stores in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="14fd7-251">Read the article from the beginning for a detailed overview of using ODBC data stores as source/sink data stores in a copy operation.</span></span>

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="14fd7-252">Troubleshoot connectivity issues</span><span class="sxs-lookup"><span data-stu-id="14fd7-252">Troubleshoot connectivity issues</span></span>

<span data-ttu-id="14fd7-253">To troubleshoot connection issues, use the **Diagnostics** tab of **Integration Runtime Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="14fd7-253">To troubleshoot connection issues, use the **Diagnostics** tab of **Integration Runtime Configuration Manager**.</span></span>

1. <span data-ttu-id="14fd7-254">Launch **Integration Runtime Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="14fd7-254">Launch **Integration Runtime Configuration Manager**.</span></span>
2. <span data-ttu-id="14fd7-255">Switch to the **Diagnostics** tab.</span><span class="sxs-lookup"><span data-stu-id="14fd7-255">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="14fd7-256">Under the "Test Connection" section, select the **type** of data store (linked service).</span><span class="sxs-lookup"><span data-stu-id="14fd7-256">Under the "Test Connection" section, select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="14fd7-257">Specify the **connection string** that is used to connect to the data store, choose the **authentication** and enter **user name**, **password**, and/or **credentials**.</span><span class="sxs-lookup"><span data-stu-id="14fd7-257">Specify the **connection string** that is used to connect to the data store, choose the **authentication** and enter **user name**, **password**, and/or **credentials**.</span></span>
5. <span data-ttu-id="14fd7-258">Click **Test connection** to test the connection to the data store.</span><span class="sxs-lookup"><span data-stu-id="14fd7-258">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14fd7-259">Next steps</span><span class="sxs-lookup"><span data-stu-id="14fd7-259">Next steps</span></span>
<span data-ttu-id="14fd7-260">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="14fd7-260">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
