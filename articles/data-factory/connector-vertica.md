---
title: Copy data from Vertica using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Vertica to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: d4399fd26c4c536f89bb15e16bfc67fb1d0940fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857151"
---
# <a name="copy-data-from-vertica-using-azure-data-factory"></a><span data-ttu-id="79cfe-103">Copy data from Vertica using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="79cfe-103">Copy data from Vertica using Azure Data Factory</span></span> 

<span data-ttu-id="79cfe-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Vertica.</span><span class="sxs-lookup"><span data-stu-id="79cfe-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Vertica.</span></span> <span data-ttu-id="79cfe-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="79cfe-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="79cfe-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="79cfe-106">Supported capabilities</span></span>

<span data-ttu-id="79cfe-107">You can copy data from Vertica to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="79cfe-107">You can copy data from Vertica to any supported sink data store.</span></span> <span data-ttu-id="79cfe-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="79cfe-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="79cfe-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="79cfe-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="79cfe-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="79cfe-110">Getting started</span></span>

<span data-ttu-id="79cfe-111">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="79cfe-111">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span></span> <span data-ttu-id="79cfe-112">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="79cfe-112">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="79cfe-113">The following sections provide details about properties that are used to define Data Factory entities specific to Vertica connector.</span><span class="sxs-lookup"><span data-stu-id="79cfe-113">The following sections provide details about properties that are used to define Data Factory entities specific to Vertica connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="79cfe-114">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="79cfe-114">Linked service properties</span></span>

<span data-ttu-id="79cfe-115">The following properties are supported for Vertica linked service:</span><span class="sxs-lookup"><span data-stu-id="79cfe-115">The following properties are supported for Vertica linked service:</span></span>

| <span data-ttu-id="79cfe-116">Property</span><span class="sxs-lookup"><span data-stu-id="79cfe-116">Property</span></span> | <span data-ttu-id="79cfe-117">Description</span><span class="sxs-lookup"><span data-stu-id="79cfe-117">Description</span></span> | <span data-ttu-id="79cfe-118">Required</span><span class="sxs-lookup"><span data-stu-id="79cfe-118">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="79cfe-119">type</span><span class="sxs-lookup"><span data-stu-id="79cfe-119">type</span></span> | <span data-ttu-id="79cfe-120">The type property must be set to: **Vertica**</span><span class="sxs-lookup"><span data-stu-id="79cfe-120">The type property must be set to: **Vertica**</span></span> | <span data-ttu-id="79cfe-121">Yes</span><span class="sxs-lookup"><span data-stu-id="79cfe-121">Yes</span></span> |
| <span data-ttu-id="79cfe-122">connectionString</span><span class="sxs-lookup"><span data-stu-id="79cfe-122">connectionString</span></span> | <span data-ttu-id="79cfe-123">An ODBC connection string to connect to Vertica.</span><span class="sxs-lookup"><span data-stu-id="79cfe-123">An ODBC connection string to connect to Vertica.</span></span> <span data-ttu-id="79cfe-124">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="79cfe-124">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="79cfe-125">Yes</span><span class="sxs-lookup"><span data-stu-id="79cfe-125">Yes</span></span> |
| <span data-ttu-id="79cfe-126">connectVia</span><span class="sxs-lookup"><span data-stu-id="79cfe-126">connectVia</span></span> | <span data-ttu-id="79cfe-127">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="79cfe-127">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="79cfe-128">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="79cfe-128">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="79cfe-129">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="79cfe-129">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="79cfe-130">No</span><span class="sxs-lookup"><span data-stu-id="79cfe-130">No</span></span> |

<span data-ttu-id="79cfe-131">**Example:**</span><span class="sxs-lookup"><span data-stu-id="79cfe-131">**Example:**</span></span>

```json
{
    "name": "VerticaLinkedService",
    "properties": {
        "type": "Vertica",
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

## <a name="dataset-properties"></a><span data-ttu-id="79cfe-132">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="79cfe-132">Dataset properties</span></span>

<span data-ttu-id="79cfe-133">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="79cfe-133">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="79cfe-134">This section provides a list of properties supported by Vertica dataset.</span><span class="sxs-lookup"><span data-stu-id="79cfe-134">This section provides a list of properties supported by Vertica dataset.</span></span>

<span data-ttu-id="79cfe-135">To copy data from Vertica, set the type property of the dataset to **VerticaTable**.</span><span class="sxs-lookup"><span data-stu-id="79cfe-135">To copy data from Vertica, set the type property of the dataset to **VerticaTable**.</span></span> <span data-ttu-id="79cfe-136">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="79cfe-136">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="79cfe-137">**Example**</span><span class="sxs-lookup"><span data-stu-id="79cfe-137">**Example**</span></span>

```json
{
    "name": "VerticaDataset",
    "properties": {
        "type": "VerticaTable",
        "linkedServiceName": {
            "referenceName": "<Vertica linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="79cfe-138">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="79cfe-138">Copy activity properties</span></span>

<span data-ttu-id="79cfe-139">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="79cfe-139">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="79cfe-140">This section provides a list of properties supported by Vertica source.</span><span class="sxs-lookup"><span data-stu-id="79cfe-140">This section provides a list of properties supported by Vertica source.</span></span>

### <a name="vertica-as-source"></a><span data-ttu-id="79cfe-141">Vertica as source</span><span class="sxs-lookup"><span data-stu-id="79cfe-141">Vertica as source</span></span>

<span data-ttu-id="79cfe-142">To copy data from Vertica, set the source type in the copy activity to **VerticaSource**.</span><span class="sxs-lookup"><span data-stu-id="79cfe-142">To copy data from Vertica, set the source type in the copy activity to **VerticaSource**.</span></span> <span data-ttu-id="79cfe-143">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="79cfe-143">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="79cfe-144">Property</span><span class="sxs-lookup"><span data-stu-id="79cfe-144">Property</span></span> | <span data-ttu-id="79cfe-145">Description</span><span class="sxs-lookup"><span data-stu-id="79cfe-145">Description</span></span> | <span data-ttu-id="79cfe-146">Required</span><span class="sxs-lookup"><span data-stu-id="79cfe-146">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="79cfe-147">type</span><span class="sxs-lookup"><span data-stu-id="79cfe-147">type</span></span> | <span data-ttu-id="79cfe-148">The type property of the copy activity source must be set to: **VerticaSource**</span><span class="sxs-lookup"><span data-stu-id="79cfe-148">The type property of the copy activity source must be set to: **VerticaSource**</span></span> | <span data-ttu-id="79cfe-149">Yes</span><span class="sxs-lookup"><span data-stu-id="79cfe-149">Yes</span></span> |
| <span data-ttu-id="79cfe-150">query</span><span class="sxs-lookup"><span data-stu-id="79cfe-150">query</span></span> | <span data-ttu-id="79cfe-151">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="79cfe-151">Use the custom SQL query to read data.</span></span> <span data-ttu-id="79cfe-152">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="79cfe-152">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="79cfe-153">Yes</span><span class="sxs-lookup"><span data-stu-id="79cfe-153">Yes</span></span> |

<span data-ttu-id="79cfe-154">**Example:**</span><span class="sxs-lookup"><span data-stu-id="79cfe-154">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromVertica",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Vertica input dataset name>",
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
                "type": "VerticaSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="79cfe-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="79cfe-155">Next steps</span></span>
<span data-ttu-id="79cfe-156">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="79cfe-156">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
