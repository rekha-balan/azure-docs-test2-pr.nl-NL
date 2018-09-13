---
title: Copy data from/to SAP Cloud for Customer using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from SAP Cloud for Customer to supported sink data stores (or) from supported source data stores to SAP Cloud for Customer by using Data Factory.
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
ms.date: 04/17/2018
ms.author: jingwang
ms.openlocfilehash: df45613105c8fb005fc8ba0c796ef768e293c57e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870068"
---
# <a name="copy-data-from-sap-cloud-for-customer-c4c-using-azure-data-factory"></a><span data-ttu-id="d30a1-103">Copy data from SAP Cloud for Customer (C4C) using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d30a1-103">Copy data from SAP Cloud for Customer (C4C) using Azure Data Factory</span></span>

<span data-ttu-id="d30a1-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from/to SAP Cloud for Customer (C4C).</span><span class="sxs-lookup"><span data-stu-id="d30a1-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from/to SAP Cloud for Customer (C4C).</span></span> <span data-ttu-id="d30a1-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="d30a1-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="d30a1-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="d30a1-106">Supported capabilities</span></span>

<span data-ttu-id="d30a1-107">You can copy data from SAP Cloud for Customer to any supported sink data store, or copy data from any supported source data store to SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="d30a1-107">You can copy data from SAP Cloud for Customer to any supported sink data store, or copy data from any supported source data store to SAP Cloud for Customer.</span></span> <span data-ttu-id="d30a1-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="d30a1-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="d30a1-109">Specifically, this connector enables Azure Data Factory to copy data from/to SAP Cloud for Customer including the SAP Cloud for Sales, SAP Cloud for Service, and SAP Cloud for Social Engagement solutions.</span><span class="sxs-lookup"><span data-stu-id="d30a1-109">Specifically, this connector enables Azure Data Factory to copy data from/to SAP Cloud for Customer including the SAP Cloud for Sales, SAP Cloud for Service, and SAP Cloud for Social Engagement solutions.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d30a1-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="d30a1-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="d30a1-111">The following sections provide details about properties that are used to define Data Factory entities specific to SAP Cloud for Customer connector.</span><span class="sxs-lookup"><span data-stu-id="d30a1-111">The following sections provide details about properties that are used to define Data Factory entities specific to SAP Cloud for Customer connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d30a1-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="d30a1-112">Linked service properties</span></span>

<span data-ttu-id="d30a1-113">The following properties are supported for SAP Cloud for Customer linked service:</span><span class="sxs-lookup"><span data-stu-id="d30a1-113">The following properties are supported for SAP Cloud for Customer linked service:</span></span>

| <span data-ttu-id="d30a1-114">Property</span><span class="sxs-lookup"><span data-stu-id="d30a1-114">Property</span></span> | <span data-ttu-id="d30a1-115">Description</span><span class="sxs-lookup"><span data-stu-id="d30a1-115">Description</span></span> | <span data-ttu-id="d30a1-116">Required</span><span class="sxs-lookup"><span data-stu-id="d30a1-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d30a1-117">type</span><span class="sxs-lookup"><span data-stu-id="d30a1-117">type</span></span> | <span data-ttu-id="d30a1-118">The type property must be set to: **SapCloudForCustomer**.</span><span class="sxs-lookup"><span data-stu-id="d30a1-118">The type property must be set to: **SapCloudForCustomer**.</span></span> | <span data-ttu-id="d30a1-119">Yes</span><span class="sxs-lookup"><span data-stu-id="d30a1-119">Yes</span></span> |
| <span data-ttu-id="d30a1-120">url</span><span class="sxs-lookup"><span data-stu-id="d30a1-120">url</span></span> | <span data-ttu-id="d30a1-121">The URL of the SAP C4C OData service.</span><span class="sxs-lookup"><span data-stu-id="d30a1-121">The URL of the SAP C4C OData service.</span></span> | <span data-ttu-id="d30a1-122">Yes</span><span class="sxs-lookup"><span data-stu-id="d30a1-122">Yes</span></span> |
| <span data-ttu-id="d30a1-123">username</span><span class="sxs-lookup"><span data-stu-id="d30a1-123">username</span></span> | <span data-ttu-id="d30a1-124">Specify the user name to connect to the SAP C4C.</span><span class="sxs-lookup"><span data-stu-id="d30a1-124">Specify the user name to connect to the SAP C4C.</span></span> | <span data-ttu-id="d30a1-125">Yes</span><span class="sxs-lookup"><span data-stu-id="d30a1-125">Yes</span></span> |
| <span data-ttu-id="d30a1-126">password</span><span class="sxs-lookup"><span data-stu-id="d30a1-126">password</span></span> | <span data-ttu-id="d30a1-127">Specify the password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="d30a1-127">Specify the password for the user account you specified for the username.</span></span> <span data-ttu-id="d30a1-128">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d30a1-128">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="d30a1-129">Yes</span><span class="sxs-lookup"><span data-stu-id="d30a1-129">Yes</span></span> |
| <span data-ttu-id="d30a1-130">connectVia</span><span class="sxs-lookup"><span data-stu-id="d30a1-130">connectVia</span></span> | <span data-ttu-id="d30a1-131">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="d30a1-131">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="d30a1-132">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d30a1-132">If not specified, it uses the default Azure Integration Runtime.</span></span> | <span data-ttu-id="d30a1-133">No for source, Yes for sink</span><span class="sxs-lookup"><span data-stu-id="d30a1-133">No for source, Yes for sink</span></span> |

>[!IMPORTANT]
><span data-ttu-id="d30a1-134">To copy data into SAP Cloud for Customer, explicitly [create an Azure IR](create-azure-integration-runtime.md#create-azure-ir) with a location near your SAP Cloud for Customer, and associate in the linked service as the following example:</span><span class="sxs-lookup"><span data-stu-id="d30a1-134">To copy data into SAP Cloud for Customer, explicitly [create an Azure IR](create-azure-integration-runtime.md#create-azure-ir) with a location near your SAP Cloud for Customer, and associate in the linked service as the following example:</span></span>

<span data-ttu-id="d30a1-135">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d30a1-135">**Example:**</span></span>

```json
{
    "name": "SAPC4CLinkedService",
    "properties": {
        "type": "SapCloudForCustomer",
        "typeProperties": {
            "url": "https://<tenantname>.crm.ondemand.com/sap/c4c/odata/v1/c4codata/" ,
            "username": "<username>",
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

## <a name="dataset-properties"></a><span data-ttu-id="d30a1-136">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="d30a1-136">Dataset properties</span></span>

<span data-ttu-id="d30a1-137">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="d30a1-137">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="d30a1-138">This section provides a list of properties supported by SAP Cloud for Customer dataset.</span><span class="sxs-lookup"><span data-stu-id="d30a1-138">This section provides a list of properties supported by SAP Cloud for Customer dataset.</span></span>

<span data-ttu-id="d30a1-139">To copy data from SAP Cloud for Customer, set the type property of the dataset to **SapCloudForCustomerResource**.</span><span class="sxs-lookup"><span data-stu-id="d30a1-139">To copy data from SAP Cloud for Customer, set the type property of the dataset to **SapCloudForCustomerResource**.</span></span> <span data-ttu-id="d30a1-140">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="d30a1-140">The following properties are supported:</span></span>

| <span data-ttu-id="d30a1-141">Property</span><span class="sxs-lookup"><span data-stu-id="d30a1-141">Property</span></span> | <span data-ttu-id="d30a1-142">Description</span><span class="sxs-lookup"><span data-stu-id="d30a1-142">Description</span></span> | <span data-ttu-id="d30a1-143">Required</span><span class="sxs-lookup"><span data-stu-id="d30a1-143">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d30a1-144">type</span><span class="sxs-lookup"><span data-stu-id="d30a1-144">type</span></span> | <span data-ttu-id="d30a1-145">The type property of the dataset must be set to: **SapCloudForCustomerResource**</span><span class="sxs-lookup"><span data-stu-id="d30a1-145">The type property of the dataset must be set to: **SapCloudForCustomerResource**</span></span> |<span data-ttu-id="d30a1-146">Yes</span><span class="sxs-lookup"><span data-stu-id="d30a1-146">Yes</span></span> |
| <span data-ttu-id="d30a1-147">path</span><span class="sxs-lookup"><span data-stu-id="d30a1-147">path</span></span> | <span data-ttu-id="d30a1-148">Specify path of the SAP C4C OData entity.</span><span class="sxs-lookup"><span data-stu-id="d30a1-148">Specify path of the SAP C4C OData entity.</span></span> |<span data-ttu-id="d30a1-149">Yes</span><span class="sxs-lookup"><span data-stu-id="d30a1-149">Yes</span></span> |

<span data-ttu-id="d30a1-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d30a1-150">**Example:**</span></span>

```json
{
    "name": "SAPC4CDataset",
    "properties": {
        "type": "SapCloudForCustomerResource",
        "typePoperties": {
            "path": "<path e.g. LeadCollection>"
        },
        "linkedServiceName": {
            "referenceName": "<SAP C4C linked service>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="d30a1-151">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="d30a1-151">Copy activity properties</span></span>

<span data-ttu-id="d30a1-152">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="d30a1-152">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="d30a1-153">This section provides a list of properties supported by SAP Cloud for Customer source.</span><span class="sxs-lookup"><span data-stu-id="d30a1-153">This section provides a list of properties supported by SAP Cloud for Customer source.</span></span>

### <a name="sap-c4c-as-source"></a><span data-ttu-id="d30a1-154">SAP C4C as source</span><span class="sxs-lookup"><span data-stu-id="d30a1-154">SAP C4C as source</span></span>

<span data-ttu-id="d30a1-155">To copy data from SAP Cloud for Customer, set the source type in the copy activity to **SapCloudForCustomerSource**.</span><span class="sxs-lookup"><span data-stu-id="d30a1-155">To copy data from SAP Cloud for Customer, set the source type in the copy activity to **SapCloudForCustomerSource**.</span></span> <span data-ttu-id="d30a1-156">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="d30a1-156">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="d30a1-157">Property</span><span class="sxs-lookup"><span data-stu-id="d30a1-157">Property</span></span> | <span data-ttu-id="d30a1-158">Description</span><span class="sxs-lookup"><span data-stu-id="d30a1-158">Description</span></span> | <span data-ttu-id="d30a1-159">Required</span><span class="sxs-lookup"><span data-stu-id="d30a1-159">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d30a1-160">type</span><span class="sxs-lookup"><span data-stu-id="d30a1-160">type</span></span> | <span data-ttu-id="d30a1-161">The type property must be set to: **SapCloudForCustomerSource**</span><span class="sxs-lookup"><span data-stu-id="d30a1-161">The type property must be set to: **SapCloudForCustomerSource**</span></span>  | <span data-ttu-id="d30a1-162">Yes</span><span class="sxs-lookup"><span data-stu-id="d30a1-162">Yes</span></span> |
| <span data-ttu-id="d30a1-163">query</span><span class="sxs-lookup"><span data-stu-id="d30a1-163">query</span></span> | <span data-ttu-id="d30a1-164">Specify the custom OData query to read data.</span><span class="sxs-lookup"><span data-stu-id="d30a1-164">Specify the custom OData query to read data.</span></span> | <span data-ttu-id="d30a1-165">No</span><span class="sxs-lookup"><span data-stu-id="d30a1-165">No</span></span> |

<span data-ttu-id="d30a1-166">Sample query to get data for a specific day: `"query": "$filter=CreatedOn ge datetimeoffset'2017-07-31T10:02:06.4202620Z' and CreatedOn le datetimeoffset'2017-08-01T10:02:06.4202620Z'"`</span><span class="sxs-lookup"><span data-stu-id="d30a1-166">Sample query to get data for a specific day: `"query": "$filter=CreatedOn ge datetimeoffset'2017-07-31T10:02:06.4202620Z' and CreatedOn le datetimeoffset'2017-08-01T10:02:06.4202620Z'"`</span></span>

<span data-ttu-id="d30a1-167">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d30a1-167">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSAPC4C",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SAP C4C input dataset>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SapCloudForCustomerSource",
                "query": "<custom query e.g. $top=10>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="sap-c4c-as-sink"></a><span data-ttu-id="d30a1-168">SAP C4C as sink</span><span class="sxs-lookup"><span data-stu-id="d30a1-168">SAP C4C as sink</span></span>

<span data-ttu-id="d30a1-169">To copy data to SAP Cloud for Customer, set the sink type in the copy activity to **SapCloudForCustomerSink**.</span><span class="sxs-lookup"><span data-stu-id="d30a1-169">To copy data to SAP Cloud for Customer, set the sink type in the copy activity to **SapCloudForCustomerSink**.</span></span> <span data-ttu-id="d30a1-170">The following properties are supported in the copy activity **sink** section:</span><span class="sxs-lookup"><span data-stu-id="d30a1-170">The following properties are supported in the copy activity **sink** section:</span></span>

| <span data-ttu-id="d30a1-171">Property</span><span class="sxs-lookup"><span data-stu-id="d30a1-171">Property</span></span> | <span data-ttu-id="d30a1-172">Description</span><span class="sxs-lookup"><span data-stu-id="d30a1-172">Description</span></span> | <span data-ttu-id="d30a1-173">Required</span><span class="sxs-lookup"><span data-stu-id="d30a1-173">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d30a1-174">type</span><span class="sxs-lookup"><span data-stu-id="d30a1-174">type</span></span> | <span data-ttu-id="d30a1-175">The type property must be set to: **SapCloudForCustomerSink**</span><span class="sxs-lookup"><span data-stu-id="d30a1-175">The type property must be set to: **SapCloudForCustomerSink**</span></span>  | <span data-ttu-id="d30a1-176">Yes</span><span class="sxs-lookup"><span data-stu-id="d30a1-176">Yes</span></span> |
| <span data-ttu-id="d30a1-177">writeBehavior</span><span class="sxs-lookup"><span data-stu-id="d30a1-177">writeBehavior</span></span> | <span data-ttu-id="d30a1-178">The write behavior of the operation.</span><span class="sxs-lookup"><span data-stu-id="d30a1-178">The write behavior of the operation.</span></span> <span data-ttu-id="d30a1-179">Could be “Insert”, “Update”.</span><span class="sxs-lookup"><span data-stu-id="d30a1-179">Could be “Insert”, “Update”.</span></span> | <span data-ttu-id="d30a1-180">No.</span><span class="sxs-lookup"><span data-stu-id="d30a1-180">No.</span></span> <span data-ttu-id="d30a1-181">Default “Insert”.</span><span class="sxs-lookup"><span data-stu-id="d30a1-181">Default “Insert”.</span></span> |
| <span data-ttu-id="d30a1-182">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d30a1-182">writeBatchSize</span></span> | <span data-ttu-id="d30a1-183">The batch size of write operation.</span><span class="sxs-lookup"><span data-stu-id="d30a1-183">The batch size of write operation.</span></span> <span data-ttu-id="d30a1-184">The batch size to get best performance may be different for different table or server.</span><span class="sxs-lookup"><span data-stu-id="d30a1-184">The batch size to get best performance may be different for different table or server.</span></span> | <span data-ttu-id="d30a1-185">No.</span><span class="sxs-lookup"><span data-stu-id="d30a1-185">No.</span></span> <span data-ttu-id="d30a1-186">Default 10.</span><span class="sxs-lookup"><span data-stu-id="d30a1-186">Default 10.</span></span> |

<span data-ttu-id="d30a1-187">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d30a1-187">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyToSapC4c",
        "type": "Copy",
        "inputs": [{
            "type": "DatasetReference",
            "referenceName": "<dataset type>"
        }],
        "outputs": [{
            "type": "DatasetReference",
            "referenceName": "SapC4cDataset"
        }],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SapCloudForCustomerSink",
                "writeBehavior": "Insert",
                "writeBatchSize": 30
            },
            "parallelCopies": 10,
            "dataIntegrationUnits": 4,
            "enableSkipIncompatibleRow": true,
            "redirectIncompatibleRowSettings": {
                "linkedServiceName": {
                    "referenceName": "ErrorLogBlobLinkedService",
                    "type": "LinkedServiceReference"
                },
                "path": "incompatiblerows"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-sap-cloud-for-customer"></a><span data-ttu-id="d30a1-188">Data type mapping for SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="d30a1-188">Data type mapping for SAP Cloud for Customer</span></span>

<span data-ttu-id="d30a1-189">When copying data from SAP Cloud for Customer, the following mappings are used from SAP Cloud for Customer data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="d30a1-189">When copying data from SAP Cloud for Customer, the following mappings are used from SAP Cloud for Customer data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="d30a1-190">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="d30a1-190">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="d30a1-191">SAP C4C OData Data Type</span><span class="sxs-lookup"><span data-stu-id="d30a1-191">SAP C4C OData Data Type</span></span> | <span data-ttu-id="d30a1-192">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="d30a1-192">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="d30a1-193">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="d30a1-193">Edm.Binary</span></span> | <span data-ttu-id="d30a1-194">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d30a1-194">Byte[]</span></span> |
| <span data-ttu-id="d30a1-195">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="d30a1-195">Edm.Boolean</span></span> | <span data-ttu-id="d30a1-196">Bool</span><span class="sxs-lookup"><span data-stu-id="d30a1-196">Bool</span></span> |
| <span data-ttu-id="d30a1-197">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="d30a1-197">Edm.Byte</span></span> | <span data-ttu-id="d30a1-198">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d30a1-198">Byte[]</span></span> |
| <span data-ttu-id="d30a1-199">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="d30a1-199">Edm.DateTime</span></span> | <span data-ttu-id="d30a1-200">DateTime</span><span class="sxs-lookup"><span data-stu-id="d30a1-200">DateTime</span></span> |
| <span data-ttu-id="d30a1-201">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="d30a1-201">Edm.Decimal</span></span> | <span data-ttu-id="d30a1-202">Decimal</span><span class="sxs-lookup"><span data-stu-id="d30a1-202">Decimal</span></span> |
| <span data-ttu-id="d30a1-203">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="d30a1-203">Edm.Double</span></span> | <span data-ttu-id="d30a1-204">Double</span><span class="sxs-lookup"><span data-stu-id="d30a1-204">Double</span></span> |
| <span data-ttu-id="d30a1-205">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="d30a1-205">Edm.Single</span></span> | <span data-ttu-id="d30a1-206">Single</span><span class="sxs-lookup"><span data-stu-id="d30a1-206">Single</span></span> |
| <span data-ttu-id="d30a1-207">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="d30a1-207">Edm.Guid</span></span> | <span data-ttu-id="d30a1-208">Guid</span><span class="sxs-lookup"><span data-stu-id="d30a1-208">Guid</span></span> |
| <span data-ttu-id="d30a1-209">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="d30a1-209">Edm.Int16</span></span> | <span data-ttu-id="d30a1-210">Int16</span><span class="sxs-lookup"><span data-stu-id="d30a1-210">Int16</span></span> |
| <span data-ttu-id="d30a1-211">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="d30a1-211">Edm.Int32</span></span> | <span data-ttu-id="d30a1-212">Int32</span><span class="sxs-lookup"><span data-stu-id="d30a1-212">Int32</span></span> |
| <span data-ttu-id="d30a1-213">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="d30a1-213">Edm.Int64</span></span> | <span data-ttu-id="d30a1-214">Int64</span><span class="sxs-lookup"><span data-stu-id="d30a1-214">Int64</span></span> |
| <span data-ttu-id="d30a1-215">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="d30a1-215">Edm.SByte</span></span> | <span data-ttu-id="d30a1-216">Int16</span><span class="sxs-lookup"><span data-stu-id="d30a1-216">Int16</span></span> |
| <span data-ttu-id="d30a1-217">Edm.String</span><span class="sxs-lookup"><span data-stu-id="d30a1-217">Edm.String</span></span> | <span data-ttu-id="d30a1-218">String</span><span class="sxs-lookup"><span data-stu-id="d30a1-218">String</span></span> |
| <span data-ttu-id="d30a1-219">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="d30a1-219">Edm.Time</span></span> | <span data-ttu-id="d30a1-220">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d30a1-220">TimeSpan</span></span> |
| <span data-ttu-id="d30a1-221">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d30a1-221">Edm.DateTimeOffset</span></span> | <span data-ttu-id="d30a1-222">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d30a1-222">DateTimeOffset</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d30a1-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="d30a1-223">Next steps</span></span>
<span data-ttu-id="d30a1-224">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d30a1-224">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
