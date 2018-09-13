---
title: Copy data from Greenplum using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Greenplum to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 12a8fb714d398db50258e2cf256379c9a3fccc55
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864365"
---
# <a name="copy-data-from-greenplum-using-azure-data-factory"></a><span data-ttu-id="72b01-103">Copy data from Greenplum using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="72b01-103">Copy data from Greenplum using Azure Data Factory</span></span> 

<span data-ttu-id="72b01-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Greenplum.</span><span class="sxs-lookup"><span data-stu-id="72b01-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Greenplum.</span></span> <span data-ttu-id="72b01-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="72b01-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="72b01-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="72b01-106">Supported capabilities</span></span>

<span data-ttu-id="72b01-107">You can copy data from Greenplum to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="72b01-107">You can copy data from Greenplum to any supported sink data store.</span></span> <span data-ttu-id="72b01-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="72b01-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="72b01-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="72b01-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="72b01-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="72b01-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="72b01-111">The following sections provide details about properties that are used to define Data Factory entities specific to Greenplum connector.</span><span class="sxs-lookup"><span data-stu-id="72b01-111">The following sections provide details about properties that are used to define Data Factory entities specific to Greenplum connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="72b01-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="72b01-112">Linked service properties</span></span>

<span data-ttu-id="72b01-113">The following properties are supported for Greenplum linked service:</span><span class="sxs-lookup"><span data-stu-id="72b01-113">The following properties are supported for Greenplum linked service:</span></span>

| <span data-ttu-id="72b01-114">Property</span><span class="sxs-lookup"><span data-stu-id="72b01-114">Property</span></span> | <span data-ttu-id="72b01-115">Description</span><span class="sxs-lookup"><span data-stu-id="72b01-115">Description</span></span> | <span data-ttu-id="72b01-116">Required</span><span class="sxs-lookup"><span data-stu-id="72b01-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="72b01-117">type</span><span class="sxs-lookup"><span data-stu-id="72b01-117">type</span></span> | <span data-ttu-id="72b01-118">The type property must be set to: **Greenplum**</span><span class="sxs-lookup"><span data-stu-id="72b01-118">The type property must be set to: **Greenplum**</span></span> | <span data-ttu-id="72b01-119">Yes</span><span class="sxs-lookup"><span data-stu-id="72b01-119">Yes</span></span> |
| <span data-ttu-id="72b01-120">connectionString</span><span class="sxs-lookup"><span data-stu-id="72b01-120">connectionString</span></span> | <span data-ttu-id="72b01-121">An ODBC connection string to connect to Greenplum.</span><span class="sxs-lookup"><span data-stu-id="72b01-121">An ODBC connection string to connect to Greenplum.</span></span> <span data-ttu-id="72b01-122">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="72b01-122">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="72b01-123">Yes</span><span class="sxs-lookup"><span data-stu-id="72b01-123">Yes</span></span> |
| <span data-ttu-id="72b01-124">connectVia</span><span class="sxs-lookup"><span data-stu-id="72b01-124">connectVia</span></span> | <span data-ttu-id="72b01-125">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="72b01-125">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="72b01-126">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="72b01-126">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="72b01-127">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="72b01-127">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="72b01-128">No</span><span class="sxs-lookup"><span data-stu-id="72b01-128">No</span></span> |

<span data-ttu-id="72b01-129">**Example:**</span><span class="sxs-lookup"><span data-stu-id="72b01-129">**Example:**</span></span>

```json
{
    "name": "GreenplumLinkedService",
    "properties": {
        "type": "Greenplum",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "HOST=<server>;PORT=<port>;DB=<database>;UID=<user name>;PWD=<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="72b01-130">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="72b01-130">Dataset properties</span></span>

<span data-ttu-id="72b01-131">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="72b01-131">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="72b01-132">This section provides a list of properties supported by Greenplum dataset.</span><span class="sxs-lookup"><span data-stu-id="72b01-132">This section provides a list of properties supported by Greenplum dataset.</span></span>

<span data-ttu-id="72b01-133">To copy data from Greenplum, set the type property of the dataset to **GreenplumTable**.</span><span class="sxs-lookup"><span data-stu-id="72b01-133">To copy data from Greenplum, set the type property of the dataset to **GreenplumTable**.</span></span> <span data-ttu-id="72b01-134">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="72b01-134">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="72b01-135">**Example**</span><span class="sxs-lookup"><span data-stu-id="72b01-135">**Example**</span></span>

```json
{
    "name": "GreenplumDataset",
    "properties": {
        "type": "GreenplumTable",
        "linkedServiceName": {
            "referenceName": "<Greenplum linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="72b01-136">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="72b01-136">Copy activity properties</span></span>

<span data-ttu-id="72b01-137">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="72b01-137">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="72b01-138">This section provides a list of properties supported by Greenplum source.</span><span class="sxs-lookup"><span data-stu-id="72b01-138">This section provides a list of properties supported by Greenplum source.</span></span>

### <a name="greenplumsource-as-source"></a><span data-ttu-id="72b01-139">GreenplumSource as source</span><span class="sxs-lookup"><span data-stu-id="72b01-139">GreenplumSource as source</span></span>

<span data-ttu-id="72b01-140">To copy data from Greenplum, set the source type in the copy activity to **GreenplumSource**.</span><span class="sxs-lookup"><span data-stu-id="72b01-140">To copy data from Greenplum, set the source type in the copy activity to **GreenplumSource**.</span></span> <span data-ttu-id="72b01-141">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="72b01-141">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="72b01-142">Property</span><span class="sxs-lookup"><span data-stu-id="72b01-142">Property</span></span> | <span data-ttu-id="72b01-143">Description</span><span class="sxs-lookup"><span data-stu-id="72b01-143">Description</span></span> | <span data-ttu-id="72b01-144">Required</span><span class="sxs-lookup"><span data-stu-id="72b01-144">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="72b01-145">type</span><span class="sxs-lookup"><span data-stu-id="72b01-145">type</span></span> | <span data-ttu-id="72b01-146">The type property of the copy activity source must be set to: **GreenplumSource**</span><span class="sxs-lookup"><span data-stu-id="72b01-146">The type property of the copy activity source must be set to: **GreenplumSource**</span></span> | <span data-ttu-id="72b01-147">Yes</span><span class="sxs-lookup"><span data-stu-id="72b01-147">Yes</span></span> |
| <span data-ttu-id="72b01-148">query</span><span class="sxs-lookup"><span data-stu-id="72b01-148">query</span></span> | <span data-ttu-id="72b01-149">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="72b01-149">Use the custom SQL query to read data.</span></span> <span data-ttu-id="72b01-150">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="72b01-150">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="72b01-151">Yes</span><span class="sxs-lookup"><span data-stu-id="72b01-151">Yes</span></span> |

<span data-ttu-id="72b01-152">**Example:**</span><span class="sxs-lookup"><span data-stu-id="72b01-152">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromGreenplum",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Greenplum input dataset name>",
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
                "type": "GreenplumSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="72b01-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="72b01-153">Next steps</span></span>
<span data-ttu-id="72b01-154">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="72b01-154">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
