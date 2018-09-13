---
title: Copy data from SAP BW using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from SAP Business Warehouse to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 08/07/2018
ms.author: jingwang
ms.openlocfilehash: 52bbf93d73af281f3959e056a4d5b959e7286cb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867156"
---
# <a name="copy-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="a8cf8-103">Copy data from SAP Business Warehouse using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a8cf8-103">Copy data from SAP Business Warehouse using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-sap-business-warehouse-connector.md)
> * [Current version](connector-sap-business-warehouse.md)

<span data-ttu-id="a8cf8-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an SAP Business Warehouse (BW).</span><span class="sxs-lookup"><span data-stu-id="a8cf8-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an SAP Business Warehouse (BW).</span></span> <span data-ttu-id="a8cf8-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="a8cf8-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="a8cf8-108">Supported capabilities</span></span>

<span data-ttu-id="a8cf8-109">You can copy data from SAP Business Warehouse to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-109">You can copy data from SAP Business Warehouse to any supported sink data store.</span></span> <span data-ttu-id="a8cf8-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="a8cf8-111">Specifically, this SAP Business Warehouse connector supports:</span><span class="sxs-lookup"><span data-stu-id="a8cf8-111">Specifically, this SAP Business Warehouse connector supports:</span></span>

- <span data-ttu-id="a8cf8-112">SAP Business Warehouse **version 7.x**.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-112">SAP Business Warehouse **version 7.x**.</span></span>
- <span data-ttu-id="a8cf8-113">Copying data from **InfoCubes and QueryCubes** (including BEx queries) using MDX queries.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-113">Copying data from **InfoCubes and QueryCubes** (including BEx queries) using MDX queries.</span></span>
- <span data-ttu-id="a8cf8-114">Copying data using basic authentication.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-114">Copying data using basic authentication.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8cf8-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8cf8-115">Prerequisites</span></span>

<span data-ttu-id="a8cf8-116">To use this SAP Business Warehouse connector, you need to:</span><span class="sxs-lookup"><span data-stu-id="a8cf8-116">To use this SAP Business Warehouse connector, you need to:</span></span>

- <span data-ttu-id="a8cf8-117">Set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-117">Set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="a8cf8-118">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-118">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span></span>
- <span data-ttu-id="a8cf8-119">Install the **SAP NetWeaver library** on the Integration Runtime machine.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-119">Install the **SAP NetWeaver library** on the Integration Runtime machine.</span></span> <span data-ttu-id="a8cf8-120">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="a8cf8-120">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="a8cf8-121">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-121">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="a8cf8-122">Make sure that you pick the **64-bit** SAP NetWeaver library which matches your Integration Runtime installation.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-122">Make sure that you pick the **64-bit** SAP NetWeaver library which matches your Integration Runtime installation.</span></span> <span data-ttu-id="a8cf8-123">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-123">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="a8cf8-124">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-124">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

>[!TIP]
>To troubleshoot connectivity issue to SAP BW, make sure:
>- All dependency libraries extracted from the NetWeaver RFC SDK are in place in the %windir%\system32 folder. Usually it has icudt34.dll, icuin34.dll, icuuc34.dll, libicudecnumber.dll, librfc32.dll, libsapucum.dll, sapcrypto.dll, sapcryto_old.dll, sapnwrfc.dll.
>- The needed ports used to connect to SAP Server are enabled on the Self-hosted IR machine, which usually are port 3300 and 3201.

## <a name="getting-started"></a><span data-ttu-id="a8cf8-129">Getting started</span><span class="sxs-lookup"><span data-stu-id="a8cf8-129">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="a8cf8-130">The following sections provide details about properties that are used to define Data Factory entities specific to SAP Business Warehouse connector.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-130">The following sections provide details about properties that are used to define Data Factory entities specific to SAP Business Warehouse connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a8cf8-131">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="a8cf8-131">Linked service properties</span></span>

<span data-ttu-id="a8cf8-132">The following properties are supported for SAP Business Warehouse (BW) linked service:</span><span class="sxs-lookup"><span data-stu-id="a8cf8-132">The following properties are supported for SAP Business Warehouse (BW) linked service:</span></span>

| <span data-ttu-id="a8cf8-133">Property</span><span class="sxs-lookup"><span data-stu-id="a8cf8-133">Property</span></span> | <span data-ttu-id="a8cf8-134">Description</span><span class="sxs-lookup"><span data-stu-id="a8cf8-134">Description</span></span> | <span data-ttu-id="a8cf8-135">Required</span><span class="sxs-lookup"><span data-stu-id="a8cf8-135">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a8cf8-136">type</span><span class="sxs-lookup"><span data-stu-id="a8cf8-136">type</span></span> | <span data-ttu-id="a8cf8-137">The type property must be set to: **SapBw**</span><span class="sxs-lookup"><span data-stu-id="a8cf8-137">The type property must be set to: **SapBw**</span></span> | <span data-ttu-id="a8cf8-138">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-138">Yes</span></span> |
| <span data-ttu-id="a8cf8-139">server</span><span class="sxs-lookup"><span data-stu-id="a8cf8-139">server</span></span> | <span data-ttu-id="a8cf8-140">Name of the server on which the SAP BW instance resides.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-140">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="a8cf8-141">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-141">Yes</span></span> |
| <span data-ttu-id="a8cf8-142">systemNumber</span><span class="sxs-lookup"><span data-stu-id="a8cf8-142">systemNumber</span></span> | <span data-ttu-id="a8cf8-143">System number of the SAP BW system.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-143">System number of the SAP BW system.</span></span><br/><span data-ttu-id="a8cf8-144">Allowed value: two-digit decimal number represented as a string.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-144">Allowed value: two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="a8cf8-145">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-145">Yes</span></span> |
| <span data-ttu-id="a8cf8-146">clientId</span><span class="sxs-lookup"><span data-stu-id="a8cf8-146">clientId</span></span> | <span data-ttu-id="a8cf8-147">Client ID of the client in the SAP W system.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-147">Client ID of the client in the SAP W system.</span></span><br/><span data-ttu-id="a8cf8-148">Allowed value: three-digit decimal number represented as a string.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-148">Allowed value: three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="a8cf8-149">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-149">Yes</span></span> |
| <span data-ttu-id="a8cf8-150">userName</span><span class="sxs-lookup"><span data-stu-id="a8cf8-150">userName</span></span> | <span data-ttu-id="a8cf8-151">Name of the user who has access to the SAP server.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-151">Name of the user who has access to the SAP server.</span></span> | <span data-ttu-id="a8cf8-152">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-152">Yes</span></span> |
| <span data-ttu-id="a8cf8-153">password</span><span class="sxs-lookup"><span data-stu-id="a8cf8-153">password</span></span> | <span data-ttu-id="a8cf8-154">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-154">Password for the user.</span></span> <span data-ttu-id="a8cf8-155">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="a8cf8-155">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="a8cf8-156">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-156">Yes</span></span> |
| <span data-ttu-id="a8cf8-157">connectVia</span><span class="sxs-lookup"><span data-stu-id="a8cf8-157">connectVia</span></span> | <span data-ttu-id="a8cf8-158">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-158">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="a8cf8-159">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="a8cf8-159">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span></span> |<span data-ttu-id="a8cf8-160">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-160">Yes</span></span> |

<span data-ttu-id="a8cf8-161">**Example:**</span><span class="sxs-lookup"><span data-stu-id="a8cf8-161">**Example:**</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "userName": "<SAP user>",
            "password": {
                "type": "SecureString",
                "value": "<Password for SAP user>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a8cf8-162">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="a8cf8-162">Dataset properties</span></span>

<span data-ttu-id="a8cf8-163">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-163">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="a8cf8-164">This section provides a list of properties supported by SAP BW dataset.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-164">This section provides a list of properties supported by SAP BW dataset.</span></span>

<span data-ttu-id="a8cf8-165">To copy data from SAP BW, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-165">To copy data from SAP BW, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="a8cf8-166">While there are no type-specific properties supported for the SAP BW dataset of type RelationalTable.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-166">While there are no type-specific properties supported for the SAP BW dataset of type RelationalTable.</span></span>

<span data-ttu-id="a8cf8-167">**Example:**</span><span class="sxs-lookup"><span data-stu-id="a8cf8-167">**Example:**</span></span>

```json
{
    "name": "SAPBWDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<SAP BW linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="a8cf8-168">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="a8cf8-168">Copy activity properties</span></span>

<span data-ttu-id="a8cf8-169">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-169">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="a8cf8-170">This section provides a list of properties supported by SAP BW source.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-170">This section provides a list of properties supported by SAP BW source.</span></span>

### <a name="sap-bw-as-source"></a><span data-ttu-id="a8cf8-171">SAP BW as source</span><span class="sxs-lookup"><span data-stu-id="a8cf8-171">SAP BW as source</span></span>

<span data-ttu-id="a8cf8-172">To copy data from SAP BW, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-172">To copy data from SAP BW, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="a8cf8-173">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="a8cf8-173">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="a8cf8-174">Property</span><span class="sxs-lookup"><span data-stu-id="a8cf8-174">Property</span></span> | <span data-ttu-id="a8cf8-175">Description</span><span class="sxs-lookup"><span data-stu-id="a8cf8-175">Description</span></span> | <span data-ttu-id="a8cf8-176">Required</span><span class="sxs-lookup"><span data-stu-id="a8cf8-176">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a8cf8-177">type</span><span class="sxs-lookup"><span data-stu-id="a8cf8-177">type</span></span> | <span data-ttu-id="a8cf8-178">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="a8cf8-178">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="a8cf8-179">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-179">Yes</span></span> |
| <span data-ttu-id="a8cf8-180">query</span><span class="sxs-lookup"><span data-stu-id="a8cf8-180">query</span></span> | <span data-ttu-id="a8cf8-181">Specifies the MDX query to read data from the SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-181">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="a8cf8-182">Yes</span><span class="sxs-lookup"><span data-stu-id="a8cf8-182">Yes</span></span> |

<span data-ttu-id="a8cf8-183">**Example:**</span><span class="sxs-lookup"><span data-stu-id="a8cf8-183">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSAPBW",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SAP BW input dataset name>",
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
                "query": "<MDX query for SAP BW>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-sap-bw"></a><span data-ttu-id="a8cf8-184">Data type mapping for SAP BW</span><span class="sxs-lookup"><span data-stu-id="a8cf8-184">Data type mapping for SAP BW</span></span>

<span data-ttu-id="a8cf8-185">When copying data from SAP BW, the following mappings are used from SAP BW data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-185">When copying data from SAP BW, the following mappings are used from SAP BW data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="a8cf8-186">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="a8cf8-186">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="a8cf8-187">SAP BW data type</span><span class="sxs-lookup"><span data-stu-id="a8cf8-187">SAP BW data type</span></span> | <span data-ttu-id="a8cf8-188">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="a8cf8-188">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8cf8-189">ACCP</span><span class="sxs-lookup"><span data-stu-id="a8cf8-189">ACCP</span></span> | <span data-ttu-id="a8cf8-190">Int</span><span class="sxs-lookup"><span data-stu-id="a8cf8-190">Int</span></span> |
| <span data-ttu-id="a8cf8-191">CHAR</span><span class="sxs-lookup"><span data-stu-id="a8cf8-191">CHAR</span></span> | <span data-ttu-id="a8cf8-192">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-192">String</span></span> |
| <span data-ttu-id="a8cf8-193">CLNT</span><span class="sxs-lookup"><span data-stu-id="a8cf8-193">CLNT</span></span> | <span data-ttu-id="a8cf8-194">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-194">String</span></span> |
| <span data-ttu-id="a8cf8-195">CURR</span><span class="sxs-lookup"><span data-stu-id="a8cf8-195">CURR</span></span> | <span data-ttu-id="a8cf8-196">Decimal</span><span class="sxs-lookup"><span data-stu-id="a8cf8-196">Decimal</span></span> |
| <span data-ttu-id="a8cf8-197">CUKY</span><span class="sxs-lookup"><span data-stu-id="a8cf8-197">CUKY</span></span> | <span data-ttu-id="a8cf8-198">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-198">String</span></span> |
| <span data-ttu-id="a8cf8-199">DEC</span><span class="sxs-lookup"><span data-stu-id="a8cf8-199">DEC</span></span> | <span data-ttu-id="a8cf8-200">Decimal</span><span class="sxs-lookup"><span data-stu-id="a8cf8-200">Decimal</span></span> |
| <span data-ttu-id="a8cf8-201">FLTP</span><span class="sxs-lookup"><span data-stu-id="a8cf8-201">FLTP</span></span> | <span data-ttu-id="a8cf8-202">Double</span><span class="sxs-lookup"><span data-stu-id="a8cf8-202">Double</span></span> |
| <span data-ttu-id="a8cf8-203">INT1</span><span class="sxs-lookup"><span data-stu-id="a8cf8-203">INT1</span></span> | <span data-ttu-id="a8cf8-204">Byte</span><span class="sxs-lookup"><span data-stu-id="a8cf8-204">Byte</span></span> |
| <span data-ttu-id="a8cf8-205">INT2</span><span class="sxs-lookup"><span data-stu-id="a8cf8-205">INT2</span></span> | <span data-ttu-id="a8cf8-206">Int16</span><span class="sxs-lookup"><span data-stu-id="a8cf8-206">Int16</span></span> |
| <span data-ttu-id="a8cf8-207">INT4</span><span class="sxs-lookup"><span data-stu-id="a8cf8-207">INT4</span></span> | <span data-ttu-id="a8cf8-208">Int</span><span class="sxs-lookup"><span data-stu-id="a8cf8-208">Int</span></span> |
| <span data-ttu-id="a8cf8-209">LANG</span><span class="sxs-lookup"><span data-stu-id="a8cf8-209">LANG</span></span> | <span data-ttu-id="a8cf8-210">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-210">String</span></span> |
| <span data-ttu-id="a8cf8-211">LCHR</span><span class="sxs-lookup"><span data-stu-id="a8cf8-211">LCHR</span></span> | <span data-ttu-id="a8cf8-212">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-212">String</span></span> |
| <span data-ttu-id="a8cf8-213">LRAW</span><span class="sxs-lookup"><span data-stu-id="a8cf8-213">LRAW</span></span> | <span data-ttu-id="a8cf8-214">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a8cf8-214">Byte[]</span></span> |
| <span data-ttu-id="a8cf8-215">PREC</span><span class="sxs-lookup"><span data-stu-id="a8cf8-215">PREC</span></span> | <span data-ttu-id="a8cf8-216">Int16</span><span class="sxs-lookup"><span data-stu-id="a8cf8-216">Int16</span></span> |
| <span data-ttu-id="a8cf8-217">QUAN</span><span class="sxs-lookup"><span data-stu-id="a8cf8-217">QUAN</span></span> | <span data-ttu-id="a8cf8-218">Decimal</span><span class="sxs-lookup"><span data-stu-id="a8cf8-218">Decimal</span></span> |
| <span data-ttu-id="a8cf8-219">RAW</span><span class="sxs-lookup"><span data-stu-id="a8cf8-219">RAW</span></span> | <span data-ttu-id="a8cf8-220">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a8cf8-220">Byte[]</span></span> |
| <span data-ttu-id="a8cf8-221">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="a8cf8-221">RAWSTRING</span></span> | <span data-ttu-id="a8cf8-222">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a8cf8-222">Byte[]</span></span> |
| <span data-ttu-id="a8cf8-223">STRING</span><span class="sxs-lookup"><span data-stu-id="a8cf8-223">STRING</span></span> | <span data-ttu-id="a8cf8-224">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-224">String</span></span> |
| <span data-ttu-id="a8cf8-225">UNIT</span><span class="sxs-lookup"><span data-stu-id="a8cf8-225">UNIT</span></span> | <span data-ttu-id="a8cf8-226">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-226">String</span></span> |
| <span data-ttu-id="a8cf8-227">DATS</span><span class="sxs-lookup"><span data-stu-id="a8cf8-227">DATS</span></span> | <span data-ttu-id="a8cf8-228">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-228">String</span></span> |
| <span data-ttu-id="a8cf8-229">NUMC</span><span class="sxs-lookup"><span data-stu-id="a8cf8-229">NUMC</span></span> | <span data-ttu-id="a8cf8-230">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-230">String</span></span> |
| <span data-ttu-id="a8cf8-231">TIMS</span><span class="sxs-lookup"><span data-stu-id="a8cf8-231">TIMS</span></span> | <span data-ttu-id="a8cf8-232">String</span><span class="sxs-lookup"><span data-stu-id="a8cf8-232">String</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a8cf8-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8cf8-233">Next steps</span></span>
<span data-ttu-id="a8cf8-234">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="a8cf8-234">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
