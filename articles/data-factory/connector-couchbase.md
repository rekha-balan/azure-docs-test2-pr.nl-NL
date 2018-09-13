---
title: Copy data from Couchbase using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Couchbase to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 9806ec19df0a68ac71cf639f5cb9b2b600a574ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968974"
---
# <a name="copy-data-from-couchbase-using-azure-data-factory"></a><span data-ttu-id="86ba8-103">Copy data from Couchbase using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="86ba8-103">Copy data from Couchbase using Azure Data Factory</span></span>

<span data-ttu-id="86ba8-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Couchbase.</span><span class="sxs-lookup"><span data-stu-id="86ba8-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Couchbase.</span></span> <span data-ttu-id="86ba8-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="86ba8-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86ba8-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="86ba8-106">This connector is currently in preview.</span></span> <span data-ttu-id="86ba8-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="86ba8-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="86ba8-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="86ba8-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="86ba8-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="86ba8-109">Supported capabilities</span></span>

<span data-ttu-id="86ba8-110">You can copy data from Couchbase to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="86ba8-110">You can copy data from Couchbase to any supported sink data store.</span></span> <span data-ttu-id="86ba8-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="86ba8-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="86ba8-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="86ba8-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="86ba8-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="86ba8-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="86ba8-114">The following sections provide details about properties that are used to define Data Factory entities specific to Couchbase connector.</span><span class="sxs-lookup"><span data-stu-id="86ba8-114">The following sections provide details about properties that are used to define Data Factory entities specific to Couchbase connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="86ba8-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="86ba8-115">Linked service properties</span></span>

<span data-ttu-id="86ba8-116">The following properties are supported for Couchbase linked service:</span><span class="sxs-lookup"><span data-stu-id="86ba8-116">The following properties are supported for Couchbase linked service:</span></span>

| <span data-ttu-id="86ba8-117">Property</span><span class="sxs-lookup"><span data-stu-id="86ba8-117">Property</span></span> | <span data-ttu-id="86ba8-118">Description</span><span class="sxs-lookup"><span data-stu-id="86ba8-118">Description</span></span> | <span data-ttu-id="86ba8-119">Required</span><span class="sxs-lookup"><span data-stu-id="86ba8-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="86ba8-120">type</span><span class="sxs-lookup"><span data-stu-id="86ba8-120">type</span></span> | <span data-ttu-id="86ba8-121">The type property must be set to: **Couchbase**</span><span class="sxs-lookup"><span data-stu-id="86ba8-121">The type property must be set to: **Couchbase**</span></span> | <span data-ttu-id="86ba8-122">Yes</span><span class="sxs-lookup"><span data-stu-id="86ba8-122">Yes</span></span> |
| <span data-ttu-id="86ba8-123">connectionString</span><span class="sxs-lookup"><span data-stu-id="86ba8-123">connectionString</span></span> | <span data-ttu-id="86ba8-124">An ODBC connection string to connect to Couchbase.</span><span class="sxs-lookup"><span data-stu-id="86ba8-124">An ODBC connection string to connect to Couchbase.</span></span> <span data-ttu-id="86ba8-125">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="86ba8-125">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="86ba8-126">Yes</span><span class="sxs-lookup"><span data-stu-id="86ba8-126">Yes</span></span> |
| <span data-ttu-id="86ba8-127">connectVia</span><span class="sxs-lookup"><span data-stu-id="86ba8-127">connectVia</span></span> | <span data-ttu-id="86ba8-128">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="86ba8-128">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="86ba8-129">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="86ba8-129">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="86ba8-130">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="86ba8-130">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="86ba8-131">No</span><span class="sxs-lookup"><span data-stu-id="86ba8-131">No</span></span> |

<span data-ttu-id="86ba8-132">**Example:**</span><span class="sxs-lookup"><span data-stu-id="86ba8-132">**Example:**</span></span>

```json
{
    "name": "CouchbaseLinkedService",
    "properties": {
        "type": "Couchbase",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<server>; Port=<port>;AuthMech=1;CredString=[{\"user\": \"JSmith\", \"pass\":\"access123\"}, {\"user\": \"Admin\", \"pass\":\"simba123\"}];"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="86ba8-133">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="86ba8-133">Dataset properties</span></span>

<span data-ttu-id="86ba8-134">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="86ba8-134">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="86ba8-135">This section provides a list of properties supported by Couchbase dataset.</span><span class="sxs-lookup"><span data-stu-id="86ba8-135">This section provides a list of properties supported by Couchbase dataset.</span></span>

<span data-ttu-id="86ba8-136">To copy data from Couchbase, set the type property of the dataset to **CouchbaseTable**.</span><span class="sxs-lookup"><span data-stu-id="86ba8-136">To copy data from Couchbase, set the type property of the dataset to **CouchbaseTable**.</span></span> <span data-ttu-id="86ba8-137">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="86ba8-137">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="86ba8-138">**Example**</span><span class="sxs-lookup"><span data-stu-id="86ba8-138">**Example**</span></span>

```json
{
    "name": "CouchbaseDataset",
    "properties": {
        "type": "CouchbaseTable",
        "linkedServiceName": {
            "referenceName": "<Couchbase linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="86ba8-139">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="86ba8-139">Copy activity properties</span></span>

<span data-ttu-id="86ba8-140">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="86ba8-140">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="86ba8-141">This section provides a list of properties supported by Couchbase source.</span><span class="sxs-lookup"><span data-stu-id="86ba8-141">This section provides a list of properties supported by Couchbase source.</span></span>

### <a name="couchbasesource-as-source"></a><span data-ttu-id="86ba8-142">CouchbaseSource as source</span><span class="sxs-lookup"><span data-stu-id="86ba8-142">CouchbaseSource as source</span></span>

<span data-ttu-id="86ba8-143">To copy data from Couchbase, set the source type in the copy activity to **CouchbaseSource**.</span><span class="sxs-lookup"><span data-stu-id="86ba8-143">To copy data from Couchbase, set the source type in the copy activity to **CouchbaseSource**.</span></span> <span data-ttu-id="86ba8-144">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="86ba8-144">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="86ba8-145">Property</span><span class="sxs-lookup"><span data-stu-id="86ba8-145">Property</span></span> | <span data-ttu-id="86ba8-146">Description</span><span class="sxs-lookup"><span data-stu-id="86ba8-146">Description</span></span> | <span data-ttu-id="86ba8-147">Required</span><span class="sxs-lookup"><span data-stu-id="86ba8-147">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="86ba8-148">type</span><span class="sxs-lookup"><span data-stu-id="86ba8-148">type</span></span> | <span data-ttu-id="86ba8-149">The type property of the copy activity source must be set to: **CouchbaseSource**</span><span class="sxs-lookup"><span data-stu-id="86ba8-149">The type property of the copy activity source must be set to: **CouchbaseSource**</span></span> | <span data-ttu-id="86ba8-150">Yes</span><span class="sxs-lookup"><span data-stu-id="86ba8-150">Yes</span></span> |
| <span data-ttu-id="86ba8-151">query</span><span class="sxs-lookup"><span data-stu-id="86ba8-151">query</span></span> | <span data-ttu-id="86ba8-152">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="86ba8-152">Use the custom SQL query to read data.</span></span> <span data-ttu-id="86ba8-153">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="86ba8-153">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="86ba8-154">Yes</span><span class="sxs-lookup"><span data-stu-id="86ba8-154">Yes</span></span> |

<span data-ttu-id="86ba8-155">**Example:**</span><span class="sxs-lookup"><span data-stu-id="86ba8-155">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromCouchbase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Couchbase input dataset name>",
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
                "type": "CouchbaseSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="86ba8-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="86ba8-156">Next steps</span></span>
<span data-ttu-id="86ba8-157">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="86ba8-157">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
