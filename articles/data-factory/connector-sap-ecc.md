---
title: Copy data from SAP ECC using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from SAP ECC to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 04/26/2018
ms.author: jingwang
ms.openlocfilehash: f9f6d2e43fff9a3e57145f39863f66eed64869b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856903"
---
# <a name="copy-data-from-sap-ecc-using-azure-data-factory"></a><span data-ttu-id="ef7b8-103">Copy data from SAP ECC using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ef7b8-103">Copy data from SAP ECC using Azure Data Factory</span></span>

<span data-ttu-id="ef7b8-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from SAP ECC (SAP Enterprise Central Component).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from SAP ECC (SAP Enterprise Central Component).</span></span> <span data-ttu-id="ef7b8-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="ef7b8-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="ef7b8-106">Supported capabilities</span></span>

<span data-ttu-id="ef7b8-107">You can copy data from SAP ECC to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-107">You can copy data from SAP ECC to any supported sink data store.</span></span> <span data-ttu-id="ef7b8-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="ef7b8-109">Specifically, this SAP ECC connector supports:</span><span class="sxs-lookup"><span data-stu-id="ef7b8-109">Specifically, this SAP ECC connector supports:</span></span>

- <span data-ttu-id="ef7b8-110">Copying data from SAP ECC on SAP NetWeaver version 7.0 and above.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-110">Copying data from SAP ECC on SAP NetWeaver version 7.0 and above.</span></span> 
- <span data-ttu-id="ef7b8-111">Copying data from any objects exposed by SAP ECC OData services (e.g. SAP Table/Views, BAPI, Data Extractors, etc.), or data/IDOCs sent to SAP PI that can be received as OData via relative Adapters.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-111">Copying data from any objects exposed by SAP ECC OData services (e.g. SAP Table/Views, BAPI, Data Extractors, etc.), or data/IDOCs sent to SAP PI that can be received as OData via relative Adapters.</span></span>
- <span data-ttu-id="ef7b8-112">Copying data using basic authentication.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-112">Copying data using basic authentication.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef7b8-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ef7b8-113">Prerequisites</span></span>

<span data-ttu-id="ef7b8-114">Generally, SAP ECC exposes entities via OData services through SAP Gateway.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-114">Generally, SAP ECC exposes entities via OData services through SAP Gateway.</span></span> <span data-ttu-id="ef7b8-115">To use this SAP ECC connector, you need to:</span><span class="sxs-lookup"><span data-stu-id="ef7b8-115">To use this SAP ECC connector, you need to:</span></span>

- <span data-ttu-id="ef7b8-116">**Set up SAP Gateway**.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-116">**Set up SAP Gateway**.</span></span> <span data-ttu-id="ef7b8-117">For servers with SAP NetWeaver version higher than 7.4, the SAP Gateway is already installed.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-117">For servers with SAP NetWeaver version higher than 7.4, the SAP Gateway is already installed.</span></span> <span data-ttu-id="ef7b8-118">Otherwise, you need to install imbedded Gateway or Gateway hub before exposing SAP ECC data through OData services.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-118">Otherwise, you need to install imbedded Gateway or Gateway hub before exposing SAP ECC data through OData services.</span></span> <span data-ttu-id="ef7b8-119">Learn how to set up SAP Gateway from [installation guide](https://help.sap.com/saphelp_gateway20sp12/helpdata/en/c3/424a2657aa4cf58df949578a56ba80/frameset.htm).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-119">Learn how to set up SAP Gateway from [installation guide](https://help.sap.com/saphelp_gateway20sp12/helpdata/en/c3/424a2657aa4cf58df949578a56ba80/frameset.htm).</span></span>

- <span data-ttu-id="ef7b8-120">**Activate and configure SAP OData service**.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-120">**Activate and configure SAP OData service**.</span></span> <span data-ttu-id="ef7b8-121">You can activate the OData Services through TCODE SICF in seconds.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-121">You can activate the OData Services through TCODE SICF in seconds.</span></span> <span data-ttu-id="ef7b8-122">You can also configure which objects needs to be exposed.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-122">You can also configure which objects needs to be exposed.</span></span> <span data-ttu-id="ef7b8-123">Here is a sample [step-by-step guidance](https://blogs.sap.com/2012/10/26/step-by-step-guide-to-build-an-odata-service-based-on-rfcs-part-1/).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-123">Here is a sample [step-by-step guidance](https://blogs.sap.com/2012/10/26/step-by-step-guide-to-build-an-odata-service-based-on-rfcs-part-1/).</span></span>

## <a name="getting-started"></a><span data-ttu-id="ef7b8-124">Getting started</span><span class="sxs-lookup"><span data-stu-id="ef7b8-124">Getting started</span></span>

<span data-ttu-id="ef7b8-125">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-125">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span></span> <span data-ttu-id="ef7b8-126">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-126">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="ef7b8-127">The following sections provide details about properties that are used to define Data Factory entities specific to SAP ECC connector.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-127">The following sections provide details about properties that are used to define Data Factory entities specific to SAP ECC connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ef7b8-128">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="ef7b8-128">Linked service properties</span></span>

<span data-ttu-id="ef7b8-129">The following properties are supported for SAP ECC linked service:</span><span class="sxs-lookup"><span data-stu-id="ef7b8-129">The following properties are supported for SAP ECC linked service:</span></span>

| <span data-ttu-id="ef7b8-130">Property</span><span class="sxs-lookup"><span data-stu-id="ef7b8-130">Property</span></span> | <span data-ttu-id="ef7b8-131">Description</span><span class="sxs-lookup"><span data-stu-id="ef7b8-131">Description</span></span> | <span data-ttu-id="ef7b8-132">Required</span><span class="sxs-lookup"><span data-stu-id="ef7b8-132">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ef7b8-133">type</span><span class="sxs-lookup"><span data-stu-id="ef7b8-133">type</span></span> | <span data-ttu-id="ef7b8-134">The type property must be set to: **SapEcc**</span><span class="sxs-lookup"><span data-stu-id="ef7b8-134">The type property must be set to: **SapEcc**</span></span> | <span data-ttu-id="ef7b8-135">Yes</span><span class="sxs-lookup"><span data-stu-id="ef7b8-135">Yes</span></span> |
| <span data-ttu-id="ef7b8-136">url</span><span class="sxs-lookup"><span data-stu-id="ef7b8-136">url</span></span> | <span data-ttu-id="ef7b8-137">The url of the SAP ECC OData service.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-137">The url of the SAP ECC OData service.</span></span> | <span data-ttu-id="ef7b8-138">Yes</span><span class="sxs-lookup"><span data-stu-id="ef7b8-138">Yes</span></span> |
| <span data-ttu-id="ef7b8-139">username</span><span class="sxs-lookup"><span data-stu-id="ef7b8-139">username</span></span> | <span data-ttu-id="ef7b8-140">The username used to connect to the SAP ECC.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-140">The username used to connect to the SAP ECC.</span></span> | <span data-ttu-id="ef7b8-141">No</span><span class="sxs-lookup"><span data-stu-id="ef7b8-141">No</span></span> |
| <span data-ttu-id="ef7b8-142">password</span><span class="sxs-lookup"><span data-stu-id="ef7b8-142">password</span></span> | <span data-ttu-id="ef7b8-143">The plaintext password used to connect to the SAP ECC.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-143">The plaintext password used to connect to the SAP ECC.</span></span> | <span data-ttu-id="ef7b8-144">No</span><span class="sxs-lookup"><span data-stu-id="ef7b8-144">No</span></span> |
| <span data-ttu-id="ef7b8-145">connectVia</span><span class="sxs-lookup"><span data-stu-id="ef7b8-145">connectVia</span></span> | <span data-ttu-id="ef7b8-146">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-146">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="ef7b8-147">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-147">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="ef7b8-148">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-148">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="ef7b8-149">No</span><span class="sxs-lookup"><span data-stu-id="ef7b8-149">No</span></span> |

<span data-ttu-id="ef7b8-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ef7b8-150">**Example:**</span></span>

```json
{
    "name": "SapECCLinkedService",
    "properties": {
        "type": "SapEcc",
        "typeProperties": {
            "url": "<SAP ECC OData url e.g. http://eccsvrname:8000/sap/opu/odata/sap/zgw100_dd02l_so_srv/>",
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        }
    },
    "connectVia": {
        "referenceName": "<name of Integration Runtime>",
        "type": "IntegrationRuntimeReference"
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="ef7b8-151">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="ef7b8-151">Dataset properties</span></span>

<span data-ttu-id="ef7b8-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="ef7b8-153">This section provides a list of properties supported by SAP ECC dataset.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-153">This section provides a list of properties supported by SAP ECC dataset.</span></span>

<span data-ttu-id="ef7b8-154">To copy data from SAP ECC, set the type property of the dataset to **SapEccResource**.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-154">To copy data from SAP ECC, set the type property of the dataset to **SapEccResource**.</span></span> <span data-ttu-id="ef7b8-155">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="ef7b8-155">The following properties are supported:</span></span>

| <span data-ttu-id="ef7b8-156">Property</span><span class="sxs-lookup"><span data-stu-id="ef7b8-156">Property</span></span> | <span data-ttu-id="ef7b8-157">Description</span><span class="sxs-lookup"><span data-stu-id="ef7b8-157">Description</span></span> | <span data-ttu-id="ef7b8-158">Required</span><span class="sxs-lookup"><span data-stu-id="ef7b8-158">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ef7b8-159">path</span><span class="sxs-lookup"><span data-stu-id="ef7b8-159">path</span></span> | <span data-ttu-id="ef7b8-160">Path of the SAP ECC OData entity.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-160">Path of the SAP ECC OData entity.</span></span> | <span data-ttu-id="ef7b8-161">Yes</span><span class="sxs-lookup"><span data-stu-id="ef7b8-161">Yes</span></span> |

<span data-ttu-id="ef7b8-162">**Example**</span><span class="sxs-lookup"><span data-stu-id="ef7b8-162">**Example**</span></span>

```json
{
    "name": "SapEccDataset",
    "properties": {
        "type": "SapEccResource",
        "typePoperties": {
            "path": "<entity path e.g. dd04tentitySet>"
        },
        "linkedServiceName": {
            "referenceName": "<SAP ECC linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="ef7b8-163">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="ef7b8-163">Copy activity properties</span></span>

<span data-ttu-id="ef7b8-164">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-164">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="ef7b8-165">This section provides a list of properties supported by SAP ECC source.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-165">This section provides a list of properties supported by SAP ECC source.</span></span>

### <a name="sap-ecc-as-source"></a><span data-ttu-id="ef7b8-166">SAP ECC as source</span><span class="sxs-lookup"><span data-stu-id="ef7b8-166">SAP ECC as source</span></span>

<span data-ttu-id="ef7b8-167">To copy data from SAP ECC, set the source type in the copy activity to **SapEccSource**.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-167">To copy data from SAP ECC, set the source type in the copy activity to **SapEccSource**.</span></span> <span data-ttu-id="ef7b8-168">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="ef7b8-168">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="ef7b8-169">Property</span><span class="sxs-lookup"><span data-stu-id="ef7b8-169">Property</span></span> | <span data-ttu-id="ef7b8-170">Description</span><span class="sxs-lookup"><span data-stu-id="ef7b8-170">Description</span></span> | <span data-ttu-id="ef7b8-171">Required</span><span class="sxs-lookup"><span data-stu-id="ef7b8-171">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ef7b8-172">type</span><span class="sxs-lookup"><span data-stu-id="ef7b8-172">type</span></span> | <span data-ttu-id="ef7b8-173">The type property of the copy activity source must be set to: **SapEccSource**</span><span class="sxs-lookup"><span data-stu-id="ef7b8-173">The type property of the copy activity source must be set to: **SapEccSource**</span></span> | <span data-ttu-id="ef7b8-174">Yes</span><span class="sxs-lookup"><span data-stu-id="ef7b8-174">Yes</span></span> |
| <span data-ttu-id="ef7b8-175">query</span><span class="sxs-lookup"><span data-stu-id="ef7b8-175">query</span></span> | <span data-ttu-id="ef7b8-176">OData query options to filter data.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-176">OData query options to filter data.</span></span> <span data-ttu-id="ef7b8-177">Example: "$select=Name,Description&$top=10".</span><span class="sxs-lookup"><span data-stu-id="ef7b8-177">Example: "$select=Name,Description&$top=10".</span></span><br/><br/><span data-ttu-id="ef7b8-178">SAP ECC connector copies data from the combined URL: (url specified in linked service)/(path specified in dataset)?(query specified in copy activity source).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-178">SAP ECC connector copies data from the combined URL: (url specified in linked service)/(path specified in dataset)?(query specified in copy activity source).</span></span> <span data-ttu-id="ef7b8-179">Refer to [OData URL components](http://www.odata.org/documentation/odata-version-3-0/url-conventions/).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-179">Refer to [OData URL components](http://www.odata.org/documentation/odata-version-3-0/url-conventions/).</span></span> | <span data-ttu-id="ef7b8-180">No</span><span class="sxs-lookup"><span data-stu-id="ef7b8-180">No</span></span> |

<span data-ttu-id="ef7b8-181">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ef7b8-181">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSAPECC",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SAP ECC input dataset name>",
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
                "type": "SapEccSource",
                "query": "$top=10"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-sap-ecc"></a><span data-ttu-id="ef7b8-182">Data type mapping for SAP ECC</span><span class="sxs-lookup"><span data-stu-id="ef7b8-182">Data type mapping for SAP ECC</span></span>

<span data-ttu-id="ef7b8-183">When copying data from SAP ECC, the following mappings are used from OData data types for SAP ECC data to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-183">When copying data from SAP ECC, the following mappings are used from OData data types for SAP ECC data to Azure Data Factory interim data types.</span></span> <span data-ttu-id="ef7b8-184">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-184">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="ef7b8-185">OData data type</span><span class="sxs-lookup"><span data-stu-id="ef7b8-185">OData data type</span></span> | <span data-ttu-id="ef7b8-186">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="ef7b8-186">Data factory interim data type</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ef7b8-187">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="ef7b8-187">Edm.Binary</span></span> | <span data-ttu-id="ef7b8-188">String</span><span class="sxs-lookup"><span data-stu-id="ef7b8-188">String</span></span> |
| <span data-ttu-id="ef7b8-189">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="ef7b8-189">Edm.Boolean</span></span> | <span data-ttu-id="ef7b8-190">Bool</span><span class="sxs-lookup"><span data-stu-id="ef7b8-190">Bool</span></span> |
| <span data-ttu-id="ef7b8-191">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="ef7b8-191">Edm.Byte</span></span> | <span data-ttu-id="ef7b8-192">String</span><span class="sxs-lookup"><span data-stu-id="ef7b8-192">String</span></span> |
| <span data-ttu-id="ef7b8-193">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="ef7b8-193">Edm.DateTime</span></span> | <span data-ttu-id="ef7b8-194">DateTime</span><span class="sxs-lookup"><span data-stu-id="ef7b8-194">DateTime</span></span> |
| <span data-ttu-id="ef7b8-195">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="ef7b8-195">Edm.Decimal</span></span> | <span data-ttu-id="ef7b8-196">Decimal</span><span class="sxs-lookup"><span data-stu-id="ef7b8-196">Decimal</span></span> |
| <span data-ttu-id="ef7b8-197">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="ef7b8-197">Edm.Double</span></span> | <span data-ttu-id="ef7b8-198">Double</span><span class="sxs-lookup"><span data-stu-id="ef7b8-198">Double</span></span> |
| <span data-ttu-id="ef7b8-199">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="ef7b8-199">Edm.Single</span></span> | <span data-ttu-id="ef7b8-200">Single</span><span class="sxs-lookup"><span data-stu-id="ef7b8-200">Single</span></span> |
| <span data-ttu-id="ef7b8-201">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="ef7b8-201">Edm.Guid</span></span> | <span data-ttu-id="ef7b8-202">String</span><span class="sxs-lookup"><span data-stu-id="ef7b8-202">String</span></span> |
| <span data-ttu-id="ef7b8-203">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="ef7b8-203">Edm.Int16</span></span> | <span data-ttu-id="ef7b8-204">Int16</span><span class="sxs-lookup"><span data-stu-id="ef7b8-204">Int16</span></span> |
| <span data-ttu-id="ef7b8-205">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="ef7b8-205">Edm.Int32</span></span> | <span data-ttu-id="ef7b8-206">Int32</span><span class="sxs-lookup"><span data-stu-id="ef7b8-206">Int32</span></span> |
| <span data-ttu-id="ef7b8-207">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="ef7b8-207">Edm.Int64</span></span> | <span data-ttu-id="ef7b8-208">Int64</span><span class="sxs-lookup"><span data-stu-id="ef7b8-208">Int64</span></span> |
| <span data-ttu-id="ef7b8-209">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="ef7b8-209">Edm.SByte</span></span> | <span data-ttu-id="ef7b8-210">Int16</span><span class="sxs-lookup"><span data-stu-id="ef7b8-210">Int16</span></span> |
| <span data-ttu-id="ef7b8-211">Edm.String</span><span class="sxs-lookup"><span data-stu-id="ef7b8-211">Edm.String</span></span> | <span data-ttu-id="ef7b8-212">String</span><span class="sxs-lookup"><span data-stu-id="ef7b8-212">String</span></span> |
| <span data-ttu-id="ef7b8-213">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="ef7b8-213">Edm.Time</span></span> | <span data-ttu-id="ef7b8-214">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ef7b8-214">TimeSpan</span></span> |
| <span data-ttu-id="ef7b8-215">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ef7b8-215">Edm.DateTimeOffset</span></span> | <span data-ttu-id="ef7b8-216">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ef7b8-216">DateTimeOffset</span></span> |

> [!NOTE]
> <span data-ttu-id="ef7b8-217">Complex data types are not supported now.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-217">Complex data types are not supported now.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef7b8-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef7b8-218">Next steps</span></span>
<span data-ttu-id="ef7b8-219">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-219">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
