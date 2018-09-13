---
title: Copy data from Netezza using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Netezza to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 06/15/2018
ms.author: jingwang
ms.openlocfilehash: f8c10e2200f830ea6e568e7b3fba1f0a6085cef2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867799"
---
# <a name="copy-data-from-netezza-using-azure-data-factory"></a><span data-ttu-id="383c3-103">Copy data from Netezza using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="383c3-103">Copy data from Netezza using Azure Data Factory</span></span> 

<span data-ttu-id="383c3-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Netezza.</span><span class="sxs-lookup"><span data-stu-id="383c3-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Netezza.</span></span> <span data-ttu-id="383c3-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="383c3-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="383c3-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="383c3-106">Supported capabilities</span></span>

<span data-ttu-id="383c3-107">You can copy data from Netezza to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="383c3-107">You can copy data from Netezza to any supported sink data store.</span></span> <span data-ttu-id="383c3-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="383c3-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="383c3-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="383c3-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="383c3-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="383c3-110">Getting started</span></span>

<span data-ttu-id="383c3-111">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="383c3-111">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span></span> <span data-ttu-id="383c3-112">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="383c3-112">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="383c3-113">The following sections provide details about properties that are used to define Data Factory entities specific to Netezza connector.</span><span class="sxs-lookup"><span data-stu-id="383c3-113">The following sections provide details about properties that are used to define Data Factory entities specific to Netezza connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="383c3-114">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="383c3-114">Linked service properties</span></span>

<span data-ttu-id="383c3-115">The following properties are supported for Netezza linked service:</span><span class="sxs-lookup"><span data-stu-id="383c3-115">The following properties are supported for Netezza linked service:</span></span>

| <span data-ttu-id="383c3-116">Property</span><span class="sxs-lookup"><span data-stu-id="383c3-116">Property</span></span> | <span data-ttu-id="383c3-117">Description</span><span class="sxs-lookup"><span data-stu-id="383c3-117">Description</span></span> | <span data-ttu-id="383c3-118">Required</span><span class="sxs-lookup"><span data-stu-id="383c3-118">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="383c3-119">type</span><span class="sxs-lookup"><span data-stu-id="383c3-119">type</span></span> | <span data-ttu-id="383c3-120">The type property must be set to: **Netezza**</span><span class="sxs-lookup"><span data-stu-id="383c3-120">The type property must be set to: **Netezza**</span></span> | <span data-ttu-id="383c3-121">Yes</span><span class="sxs-lookup"><span data-stu-id="383c3-121">Yes</span></span> |
| <span data-ttu-id="383c3-122">connectionString</span><span class="sxs-lookup"><span data-stu-id="383c3-122">connectionString</span></span> | <span data-ttu-id="383c3-123">An ODBC connection string to connect to Netezza.</span><span class="sxs-lookup"><span data-stu-id="383c3-123">An ODBC connection string to connect to Netezza.</span></span> <span data-ttu-id="383c3-124">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="383c3-124">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="383c3-125">Yes</span><span class="sxs-lookup"><span data-stu-id="383c3-125">Yes</span></span> |
| <span data-ttu-id="383c3-126">connectVia</span><span class="sxs-lookup"><span data-stu-id="383c3-126">connectVia</span></span> | <span data-ttu-id="383c3-127">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="383c3-127">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="383c3-128">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="383c3-128">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="383c3-129">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="383c3-129">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="383c3-130">No</span><span class="sxs-lookup"><span data-stu-id="383c3-130">No</span></span> |

<span data-ttu-id="383c3-131">A typical connection string is `Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>`.</span><span class="sxs-lookup"><span data-stu-id="383c3-131">A typical connection string is `Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>`.</span></span> <span data-ttu-id="383c3-132">More properties you can set per your case:</span><span class="sxs-lookup"><span data-stu-id="383c3-132">More properties you can set per your case:</span></span>

| <span data-ttu-id="383c3-133">Property</span><span class="sxs-lookup"><span data-stu-id="383c3-133">Property</span></span> | <span data-ttu-id="383c3-134">Description</span><span class="sxs-lookup"><span data-stu-id="383c3-134">Description</span></span> | <span data-ttu-id="383c3-135">Required</span><span class="sxs-lookup"><span data-stu-id="383c3-135">Required</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="383c3-136">SecurityLevel</span><span class="sxs-lookup"><span data-stu-id="383c3-136">SecurityLevel</span></span> | <span data-ttu-id="383c3-137">The level of security (SSL/TLS) that the driver uses for the connection to the data store.</span><span class="sxs-lookup"><span data-stu-id="383c3-137">The level of security (SSL/TLS) that the driver uses for the connection to the data store.</span></span> <span data-ttu-id="383c3-138">E.g.</span><span class="sxs-lookup"><span data-stu-id="383c3-138">E.g.</span></span> <span data-ttu-id="383c3-139">`SecurityLevel=preferredSecured`.</span><span class="sxs-lookup"><span data-stu-id="383c3-139">`SecurityLevel=preferredSecured`.</span></span> <span data-ttu-id="383c3-140">Supported values are:</span><span class="sxs-lookup"><span data-stu-id="383c3-140">Supported values are:</span></span><br/><span data-ttu-id="383c3-141">- Only Unsecured (**onlyUnSecured**): The driver does not use SSL.</span><span class="sxs-lookup"><span data-stu-id="383c3-141">- Only Unsecured (**onlyUnSecured**): The driver does not use SSL.</span></span><br/><span data-ttu-id="383c3-142">- **Preferred Unsecured (preferredUnSecured) (default)**: If the server provides a choice, the driver does not use SSL.</span><span class="sxs-lookup"><span data-stu-id="383c3-142">- **Preferred Unsecured (preferredUnSecured) (default)**: If the server provides a choice, the driver does not use SSL.</span></span> <br/><span data-ttu-id="383c3-143">- **Preferred Secured (preferredSecured)**: If the server provides a choice, the driver uses SSL.</span><span class="sxs-lookup"><span data-stu-id="383c3-143">- **Preferred Secured (preferredSecured)**: If the server provides a choice, the driver uses SSL.</span></span> <br/><span data-ttu-id="383c3-144">- **Only Secured (onlySecured)**: The driver does not connect unless an SSL connection is available</span><span class="sxs-lookup"><span data-stu-id="383c3-144">- **Only Secured (onlySecured)**: The driver does not connect unless an SSL connection is available</span></span> | <span data-ttu-id="383c3-145">No</span><span class="sxs-lookup"><span data-stu-id="383c3-145">No</span></span> |
| <span data-ttu-id="383c3-146">CaCertFile</span><span class="sxs-lookup"><span data-stu-id="383c3-146">CaCertFile</span></span> | <span data-ttu-id="383c3-147">The full path to the SSL certificate that is used by the server.</span><span class="sxs-lookup"><span data-stu-id="383c3-147">The full path to the SSL certificate that is used by the server.</span></span> <span data-ttu-id="383c3-148">E.g.</span><span class="sxs-lookup"><span data-stu-id="383c3-148">E.g.</span></span> `CaCertFile=<cert path>;`| <span data-ttu-id="383c3-149">Yes, if SSL is enabled</span><span class="sxs-lookup"><span data-stu-id="383c3-149">Yes, if SSL is enabled</span></span> |

<span data-ttu-id="383c3-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="383c3-150">**Example:**</span></span>

```json
{
    "name": "NetezzaLinkedService",
    "properties": {
        "type": "Netezza",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="383c3-151">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="383c3-151">Dataset properties</span></span>

<span data-ttu-id="383c3-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="383c3-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="383c3-153">This section provides a list of properties supported by Netezza dataset.</span><span class="sxs-lookup"><span data-stu-id="383c3-153">This section provides a list of properties supported by Netezza dataset.</span></span>

<span data-ttu-id="383c3-154">To copy data from Netezza, set the type property of the dataset to **NetezzaTable**.</span><span class="sxs-lookup"><span data-stu-id="383c3-154">To copy data from Netezza, set the type property of the dataset to **NetezzaTable**.</span></span> <span data-ttu-id="383c3-155">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="383c3-155">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="383c3-156">**Example**</span><span class="sxs-lookup"><span data-stu-id="383c3-156">**Example**</span></span>

```json
{
    "name": "NetezzaDataset",
    "properties": {
        "type": "NetezzaTable",
        "linkedServiceName": {
            "referenceName": "<Netezza linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="383c3-157">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="383c3-157">Copy activity properties</span></span>

<span data-ttu-id="383c3-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="383c3-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="383c3-159">This section provides a list of properties supported by Netezza source.</span><span class="sxs-lookup"><span data-stu-id="383c3-159">This section provides a list of properties supported by Netezza source.</span></span>

### <a name="netezza-as-source"></a><span data-ttu-id="383c3-160">Netezza as source</span><span class="sxs-lookup"><span data-stu-id="383c3-160">Netezza as source</span></span>

<span data-ttu-id="383c3-161">To copy data from Netezza, set the source type in the copy activity to **NetezzaSource**.</span><span class="sxs-lookup"><span data-stu-id="383c3-161">To copy data from Netezza, set the source type in the copy activity to **NetezzaSource**.</span></span> <span data-ttu-id="383c3-162">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="383c3-162">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="383c3-163">Property</span><span class="sxs-lookup"><span data-stu-id="383c3-163">Property</span></span> | <span data-ttu-id="383c3-164">Description</span><span class="sxs-lookup"><span data-stu-id="383c3-164">Description</span></span> | <span data-ttu-id="383c3-165">Required</span><span class="sxs-lookup"><span data-stu-id="383c3-165">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="383c3-166">type</span><span class="sxs-lookup"><span data-stu-id="383c3-166">type</span></span> | <span data-ttu-id="383c3-167">The type property of the copy activity source must be set to: **NetezzaSource**</span><span class="sxs-lookup"><span data-stu-id="383c3-167">The type property of the copy activity source must be set to: **NetezzaSource**</span></span> | <span data-ttu-id="383c3-168">Yes</span><span class="sxs-lookup"><span data-stu-id="383c3-168">Yes</span></span> |
| <span data-ttu-id="383c3-169">query</span><span class="sxs-lookup"><span data-stu-id="383c3-169">query</span></span> | <span data-ttu-id="383c3-170">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="383c3-170">Use the custom SQL query to read data.</span></span> <span data-ttu-id="383c3-171">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="383c3-171">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="383c3-172">Yes</span><span class="sxs-lookup"><span data-stu-id="383c3-172">Yes</span></span> |

<span data-ttu-id="383c3-173">**Example:**</span><span class="sxs-lookup"><span data-stu-id="383c3-173">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromNetezza",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Netezza input dataset name>",
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
                "type": "NetezzaSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="383c3-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="383c3-174">Next steps</span></span>
<span data-ttu-id="383c3-175">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="383c3-175">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
