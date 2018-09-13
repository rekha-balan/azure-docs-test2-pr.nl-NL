---
title: Copy data from OData sources using Azure Data Factory | Microsoft Docs
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
ms.date: 05/22/2018
ms.author: jingwang
ms.openlocfilehash: aaec710dd6c12f96a479a1f41603351512da1df6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868343"
---
# <a name="copy-data-from-odata-source-using-azure-data-factory"></a><span data-ttu-id="df3b1-103">Copy data from OData source using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="df3b1-103">Copy data from OData source using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-odata-connector.md)
> * [Current version](connector-odata.md)

<span data-ttu-id="df3b1-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an OData source.</span><span class="sxs-lookup"><span data-stu-id="df3b1-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an OData source.</span></span> <span data-ttu-id="df3b1-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="df3b1-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="df3b1-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="df3b1-108">Supported capabilities</span></span>

<span data-ttu-id="df3b1-109">You can copy data from OData source to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="df3b1-109">You can copy data from OData source to any supported sink data store.</span></span> <span data-ttu-id="df3b1-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="df3b1-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="df3b1-111">Specifically, this OData connector supports:</span><span class="sxs-lookup"><span data-stu-id="df3b1-111">Specifically, this OData connector supports:</span></span>

- <span data-ttu-id="df3b1-112">OData **version 3.0 and 4.0**.</span><span class="sxs-lookup"><span data-stu-id="df3b1-112">OData **version 3.0 and 4.0**.</span></span>
- <span data-ttu-id="df3b1-113">Copying data using the following authentications: **Anonymous**, **Basic**, and **Windows**.</span><span class="sxs-lookup"><span data-stu-id="df3b1-113">Copying data using the following authentications: **Anonymous**, **Basic**, and **Windows**.</span></span>

## <a name="getting-started"></a><span data-ttu-id="df3b1-114">Getting started</span><span class="sxs-lookup"><span data-stu-id="df3b1-114">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="df3b1-115">The following sections provide details about properties that are used to define Data Factory entities specific to OData connector.</span><span class="sxs-lookup"><span data-stu-id="df3b1-115">The following sections provide details about properties that are used to define Data Factory entities specific to OData connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="df3b1-116">Linked Service properties</span><span class="sxs-lookup"><span data-stu-id="df3b1-116">Linked Service properties</span></span>

<span data-ttu-id="df3b1-117">The following properties are supported for OData linked service:</span><span class="sxs-lookup"><span data-stu-id="df3b1-117">The following properties are supported for OData linked service:</span></span>

| <span data-ttu-id="df3b1-118">Property</span><span class="sxs-lookup"><span data-stu-id="df3b1-118">Property</span></span> | <span data-ttu-id="df3b1-119">Description</span><span class="sxs-lookup"><span data-stu-id="df3b1-119">Description</span></span> | <span data-ttu-id="df3b1-120">Required</span><span class="sxs-lookup"><span data-stu-id="df3b1-120">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="df3b1-121">type</span><span class="sxs-lookup"><span data-stu-id="df3b1-121">type</span></span> | <span data-ttu-id="df3b1-122">The type property must be set to: **OData**</span><span class="sxs-lookup"><span data-stu-id="df3b1-122">The type property must be set to: **OData**</span></span> |<span data-ttu-id="df3b1-123">Yes</span><span class="sxs-lookup"><span data-stu-id="df3b1-123">Yes</span></span> |
| <span data-ttu-id="df3b1-124">url</span><span class="sxs-lookup"><span data-stu-id="df3b1-124">url</span></span> | <span data-ttu-id="df3b1-125">Root URL of the OData service.</span><span class="sxs-lookup"><span data-stu-id="df3b1-125">Root URL of the OData service.</span></span> |<span data-ttu-id="df3b1-126">Yes</span><span class="sxs-lookup"><span data-stu-id="df3b1-126">Yes</span></span> |
| <span data-ttu-id="df3b1-127">authenticationType</span><span class="sxs-lookup"><span data-stu-id="df3b1-127">authenticationType</span></span> | <span data-ttu-id="df3b1-128">Type of authentication used to connect to the OData source.</span><span class="sxs-lookup"><span data-stu-id="df3b1-128">Type of authentication used to connect to the OData source.</span></span><br/><span data-ttu-id="df3b1-129">Allowed values are: **Anonymous**, **Basic**, and **Windows**.</span><span class="sxs-lookup"><span data-stu-id="df3b1-129">Allowed values are: **Anonymous**, **Basic**, and **Windows**.</span></span> <span data-ttu-id="df3b1-130">Note OAuth is not supported.</span><span class="sxs-lookup"><span data-stu-id="df3b1-130">Note OAuth is not supported.</span></span> | <span data-ttu-id="df3b1-131">Yes</span><span class="sxs-lookup"><span data-stu-id="df3b1-131">Yes</span></span> |
| <span data-ttu-id="df3b1-132">userName</span><span class="sxs-lookup"><span data-stu-id="df3b1-132">userName</span></span> | <span data-ttu-id="df3b1-133">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="df3b1-133">Specify user name if you are using Basic or Windows authentication.</span></span> | <span data-ttu-id="df3b1-134">No</span><span class="sxs-lookup"><span data-stu-id="df3b1-134">No</span></span> |
| <span data-ttu-id="df3b1-135">password</span><span class="sxs-lookup"><span data-stu-id="df3b1-135">password</span></span> | <span data-ttu-id="df3b1-136">Specify password for the user account you specified for the userName.</span><span class="sxs-lookup"><span data-stu-id="df3b1-136">Specify password for the user account you specified for the userName.</span></span> <span data-ttu-id="df3b1-137">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="df3b1-137">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="df3b1-138">No</span><span class="sxs-lookup"><span data-stu-id="df3b1-138">No</span></span> |
| <span data-ttu-id="df3b1-139">connectVia</span><span class="sxs-lookup"><span data-stu-id="df3b1-139">connectVia</span></span> | <span data-ttu-id="df3b1-140">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="df3b1-140">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="df3b1-141">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="df3b1-141">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="df3b1-142">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="df3b1-142">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="df3b1-143">No</span><span class="sxs-lookup"><span data-stu-id="df3b1-143">No</span></span> |

<span data-ttu-id="df3b1-144">**Example 1: using Anonymous authentication**</span><span class="sxs-lookup"><span data-stu-id="df3b1-144">**Example 1: using Anonymous authentication**</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="df3b1-145">**Example 2: using Basic authentication**</span><span class="sxs-lookup"><span data-stu-id="df3b1-145">**Example 2: using Basic authentication**</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of OData source>",
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

<span data-ttu-id="df3b1-146">**Example 3: using Windows authentication**</span><span class="sxs-lookup"><span data-stu-id="df3b1-146">**Example 3: using Windows authentication**</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source>",
            "authenticationType": "Windows",
            "userName": "<domain>\\<user>",
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

## <a name="dataset-properties"></a><span data-ttu-id="df3b1-147">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="df3b1-147">Dataset properties</span></span>

<span data-ttu-id="df3b1-148">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="df3b1-148">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="df3b1-149">This section provides a list of properties supported by OData dataset.</span><span class="sxs-lookup"><span data-stu-id="df3b1-149">This section provides a list of properties supported by OData dataset.</span></span>

<span data-ttu-id="df3b1-150">To copy data from OData, set the type property of the dataset to **ODataResource**.</span><span class="sxs-lookup"><span data-stu-id="df3b1-150">To copy data from OData, set the type property of the dataset to **ODataResource**.</span></span> <span data-ttu-id="df3b1-151">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="df3b1-151">The following properties are supported:</span></span>

| <span data-ttu-id="df3b1-152">Property</span><span class="sxs-lookup"><span data-stu-id="df3b1-152">Property</span></span> | <span data-ttu-id="df3b1-153">Description</span><span class="sxs-lookup"><span data-stu-id="df3b1-153">Description</span></span> | <span data-ttu-id="df3b1-154">Required</span><span class="sxs-lookup"><span data-stu-id="df3b1-154">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="df3b1-155">type</span><span class="sxs-lookup"><span data-stu-id="df3b1-155">type</span></span> | <span data-ttu-id="df3b1-156">The type property of the dataset must be set to: **ODataResource**</span><span class="sxs-lookup"><span data-stu-id="df3b1-156">The type property of the dataset must be set to: **ODataResource**</span></span> | <span data-ttu-id="df3b1-157">Yes</span><span class="sxs-lookup"><span data-stu-id="df3b1-157">Yes</span></span> |
| <span data-ttu-id="df3b1-158">path</span><span class="sxs-lookup"><span data-stu-id="df3b1-158">path</span></span> | <span data-ttu-id="df3b1-159">Path to the OData resource.</span><span class="sxs-lookup"><span data-stu-id="df3b1-159">Path to the OData resource.</span></span> | <span data-ttu-id="df3b1-160">Yes</span><span class="sxs-lookup"><span data-stu-id="df3b1-160">Yes</span></span> |

<span data-ttu-id="df3b1-161">**Example**</span><span class="sxs-lookup"><span data-stu-id="df3b1-161">**Example**</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "linkedServiceName": {
            "referenceName": "<OData linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties":
        {
            "path": "Products"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="df3b1-162">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="df3b1-162">Copy activity properties</span></span>

<span data-ttu-id="df3b1-163">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="df3b1-163">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="df3b1-164">This section provides a list of properties supported by OData source.</span><span class="sxs-lookup"><span data-stu-id="df3b1-164">This section provides a list of properties supported by OData source.</span></span>

### <a name="odata-as-source"></a><span data-ttu-id="df3b1-165">OData as source</span><span class="sxs-lookup"><span data-stu-id="df3b1-165">OData as source</span></span>

<span data-ttu-id="df3b1-166">To copy data from OData, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="df3b1-166">To copy data from OData, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="df3b1-167">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="df3b1-167">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="df3b1-168">Property</span><span class="sxs-lookup"><span data-stu-id="df3b1-168">Property</span></span> | <span data-ttu-id="df3b1-169">Description</span><span class="sxs-lookup"><span data-stu-id="df3b1-169">Description</span></span> | <span data-ttu-id="df3b1-170">Required</span><span class="sxs-lookup"><span data-stu-id="df3b1-170">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="df3b1-171">type</span><span class="sxs-lookup"><span data-stu-id="df3b1-171">type</span></span> | <span data-ttu-id="df3b1-172">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="df3b1-172">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="df3b1-173">Yes</span><span class="sxs-lookup"><span data-stu-id="df3b1-173">Yes</span></span> |
| <span data-ttu-id="df3b1-174">query</span><span class="sxs-lookup"><span data-stu-id="df3b1-174">query</span></span> | <span data-ttu-id="df3b1-175">OData query options to filter data.</span><span class="sxs-lookup"><span data-stu-id="df3b1-175">OData query options to filter data.</span></span> <span data-ttu-id="df3b1-176">Example: "?$select=Name,Description&$top=5".</span><span class="sxs-lookup"><span data-stu-id="df3b1-176">Example: "?$select=Name,Description&$top=5".</span></span><br/><br/><span data-ttu-id="df3b1-177">Note at last, OData connector copies data from the combined URL: `[url specified in linked service]/[path specified in dataset][query specified in copy activity source]`.</span><span class="sxs-lookup"><span data-stu-id="df3b1-177">Note at last, OData connector copies data from the combined URL: `[url specified in linked service]/[path specified in dataset][query specified in copy activity source]`.</span></span> <span data-ttu-id="df3b1-178">Refer to [OData URL components](http://www.odata.org/documentation/odata-version-3-0/url-conventions/).</span><span class="sxs-lookup"><span data-stu-id="df3b1-178">Refer to [OData URL components](http://www.odata.org/documentation/odata-version-3-0/url-conventions/).</span></span> | <span data-ttu-id="df3b1-179">No</span><span class="sxs-lookup"><span data-stu-id="df3b1-179">No</span></span> |

<span data-ttu-id="df3b1-180">**Example:**</span><span class="sxs-lookup"><span data-stu-id="df3b1-180">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromOData",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<OData input dataset name>",
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
                "query": "?$select=Name,Description&$top=5"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-odata"></a><span data-ttu-id="df3b1-181">Data type mapping for OData</span><span class="sxs-lookup"><span data-stu-id="df3b1-181">Data type mapping for OData</span></span>

<span data-ttu-id="df3b1-182">When copying data from OData, the following mappings are used from OData data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="df3b1-182">When copying data from OData, the following mappings are used from OData data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="df3b1-183">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="df3b1-183">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="df3b1-184">OData data type</span><span class="sxs-lookup"><span data-stu-id="df3b1-184">OData data type</span></span> | <span data-ttu-id="df3b1-185">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="df3b1-185">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="df3b1-186">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="df3b1-186">Edm.Binary</span></span> | <span data-ttu-id="df3b1-187">Byte[]</span><span class="sxs-lookup"><span data-stu-id="df3b1-187">Byte[]</span></span> |
| <span data-ttu-id="df3b1-188">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="df3b1-188">Edm.Boolean</span></span> | <span data-ttu-id="df3b1-189">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b1-189">Bool</span></span> |
| <span data-ttu-id="df3b1-190">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="df3b1-190">Edm.Byte</span></span> | <span data-ttu-id="df3b1-191">Byte[]</span><span class="sxs-lookup"><span data-stu-id="df3b1-191">Byte[]</span></span> |
| <span data-ttu-id="df3b1-192">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="df3b1-192">Edm.DateTime</span></span> | <span data-ttu-id="df3b1-193">DateTime</span><span class="sxs-lookup"><span data-stu-id="df3b1-193">DateTime</span></span> |
| <span data-ttu-id="df3b1-194">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="df3b1-194">Edm.Decimal</span></span> | <span data-ttu-id="df3b1-195">Decimal</span><span class="sxs-lookup"><span data-stu-id="df3b1-195">Decimal</span></span> |
| <span data-ttu-id="df3b1-196">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="df3b1-196">Edm.Double</span></span> | <span data-ttu-id="df3b1-197">Double</span><span class="sxs-lookup"><span data-stu-id="df3b1-197">Double</span></span> |
| <span data-ttu-id="df3b1-198">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="df3b1-198">Edm.Single</span></span> | <span data-ttu-id="df3b1-199">Single</span><span class="sxs-lookup"><span data-stu-id="df3b1-199">Single</span></span> |
| <span data-ttu-id="df3b1-200">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="df3b1-200">Edm.Guid</span></span> | <span data-ttu-id="df3b1-201">Guid</span><span class="sxs-lookup"><span data-stu-id="df3b1-201">Guid</span></span> |
| <span data-ttu-id="df3b1-202">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="df3b1-202">Edm.Int16</span></span> | <span data-ttu-id="df3b1-203">Int16</span><span class="sxs-lookup"><span data-stu-id="df3b1-203">Int16</span></span> |
| <span data-ttu-id="df3b1-204">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="df3b1-204">Edm.Int32</span></span> | <span data-ttu-id="df3b1-205">Int32</span><span class="sxs-lookup"><span data-stu-id="df3b1-205">Int32</span></span> |
| <span data-ttu-id="df3b1-206">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="df3b1-206">Edm.Int64</span></span> | <span data-ttu-id="df3b1-207">Int64</span><span class="sxs-lookup"><span data-stu-id="df3b1-207">Int64</span></span> |
| <span data-ttu-id="df3b1-208">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="df3b1-208">Edm.SByte</span></span> | <span data-ttu-id="df3b1-209">Int16</span><span class="sxs-lookup"><span data-stu-id="df3b1-209">Int16</span></span> |
| <span data-ttu-id="df3b1-210">Edm.String</span><span class="sxs-lookup"><span data-stu-id="df3b1-210">Edm.String</span></span> | <span data-ttu-id="df3b1-211">String</span><span class="sxs-lookup"><span data-stu-id="df3b1-211">String</span></span> |
| <span data-ttu-id="df3b1-212">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="df3b1-212">Edm.Time</span></span> | <span data-ttu-id="df3b1-213">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="df3b1-213">TimeSpan</span></span> |
| <span data-ttu-id="df3b1-214">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="df3b1-214">Edm.DateTimeOffset</span></span> | <span data-ttu-id="df3b1-215">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="df3b1-215">DateTimeOffset</span></span> |

> [!Note]
> OData complex data types (such as Object) are not supported.


## <a name="next-steps"></a><span data-ttu-id="df3b1-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="df3b1-217">Next steps</span></span>
<span data-ttu-id="df3b1-218">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="df3b1-218">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
