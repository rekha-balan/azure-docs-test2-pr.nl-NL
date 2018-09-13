---
title: Copy data from Drill using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Drill to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 31dcae5dde53a9a3933c15dcf3b6869ec943cbea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870810"
---
# <a name="copy-data-from-drill-using-azure-data-factory"></a><span data-ttu-id="d31f7-103">Copy data from Drill using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d31f7-103">Copy data from Drill using Azure Data Factory</span></span>

<span data-ttu-id="d31f7-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Drill.</span><span class="sxs-lookup"><span data-stu-id="d31f7-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Drill.</span></span> <span data-ttu-id="d31f7-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="d31f7-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d31f7-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="d31f7-106">This connector is currently in preview.</span></span> <span data-ttu-id="d31f7-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="d31f7-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="d31f7-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="d31f7-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="d31f7-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="d31f7-109">Supported capabilities</span></span>

<span data-ttu-id="d31f7-110">You can copy data from Drill to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="d31f7-110">You can copy data from Drill to any supported sink data store.</span></span> <span data-ttu-id="d31f7-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="d31f7-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="d31f7-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="d31f7-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d31f7-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="d31f7-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="d31f7-114">The following sections provide details about properties that are used to define Data Factory entities specific to Drill connector.</span><span class="sxs-lookup"><span data-stu-id="d31f7-114">The following sections provide details about properties that are used to define Data Factory entities specific to Drill connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d31f7-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="d31f7-115">Linked service properties</span></span>

<span data-ttu-id="d31f7-116">The following properties are supported for Drill linked service:</span><span class="sxs-lookup"><span data-stu-id="d31f7-116">The following properties are supported for Drill linked service:</span></span>

| <span data-ttu-id="d31f7-117">Property</span><span class="sxs-lookup"><span data-stu-id="d31f7-117">Property</span></span> | <span data-ttu-id="d31f7-118">Description</span><span class="sxs-lookup"><span data-stu-id="d31f7-118">Description</span></span> | <span data-ttu-id="d31f7-119">Required</span><span class="sxs-lookup"><span data-stu-id="d31f7-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d31f7-120">type</span><span class="sxs-lookup"><span data-stu-id="d31f7-120">type</span></span> | <span data-ttu-id="d31f7-121">The type property must be set to: **Drill**</span><span class="sxs-lookup"><span data-stu-id="d31f7-121">The type property must be set to: **Drill**</span></span> | <span data-ttu-id="d31f7-122">Yes</span><span class="sxs-lookup"><span data-stu-id="d31f7-122">Yes</span></span> |
| <span data-ttu-id="d31f7-123">connectionString</span><span class="sxs-lookup"><span data-stu-id="d31f7-123">connectionString</span></span> | <span data-ttu-id="d31f7-124">An ODBC connection string to connect to Drill.</span><span class="sxs-lookup"><span data-stu-id="d31f7-124">An ODBC connection string to connect to Drill.</span></span> <span data-ttu-id="d31f7-125">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d31f7-125">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="d31f7-126">Yes</span><span class="sxs-lookup"><span data-stu-id="d31f7-126">Yes</span></span> |
| <span data-ttu-id="d31f7-127">connectVia</span><span class="sxs-lookup"><span data-stu-id="d31f7-127">connectVia</span></span> | <span data-ttu-id="d31f7-128">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="d31f7-128">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="d31f7-129">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="d31f7-129">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="d31f7-130">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d31f7-130">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="d31f7-131">No</span><span class="sxs-lookup"><span data-stu-id="d31f7-131">No</span></span> |

<span data-ttu-id="d31f7-132">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d31f7-132">**Example:**</span></span>

```json
{
    "name": "DrillLinkedService",
    "properties": {
        "type": "Drill",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "ConnectionType=Direct;Host=<host>;Port=<port>;AuthenticationType=Plain;UID=<user name>;PWD=<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d31f7-133">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="d31f7-133">Dataset properties</span></span>

<span data-ttu-id="d31f7-134">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="d31f7-134">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="d31f7-135">This section provides a list of properties supported by Drill dataset.</span><span class="sxs-lookup"><span data-stu-id="d31f7-135">This section provides a list of properties supported by Drill dataset.</span></span>

<span data-ttu-id="d31f7-136">To copy data from Drill, set the type property of the dataset to **DrillTable**.</span><span class="sxs-lookup"><span data-stu-id="d31f7-136">To copy data from Drill, set the type property of the dataset to **DrillTable**.</span></span> <span data-ttu-id="d31f7-137">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="d31f7-137">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="d31f7-138">**Example**</span><span class="sxs-lookup"><span data-stu-id="d31f7-138">**Example**</span></span>

```json
{
    "name": "DrillDataset",
    "properties": {
        "type": "DrillTable",
        "linkedServiceName": {
            "referenceName": "<Drill linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="d31f7-139">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="d31f7-139">Copy activity properties</span></span>

<span data-ttu-id="d31f7-140">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="d31f7-140">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="d31f7-141">This section provides a list of properties supported by Drill source.</span><span class="sxs-lookup"><span data-stu-id="d31f7-141">This section provides a list of properties supported by Drill source.</span></span>

### <a name="drillsource-as-source"></a><span data-ttu-id="d31f7-142">DrillSource as source</span><span class="sxs-lookup"><span data-stu-id="d31f7-142">DrillSource as source</span></span>

<span data-ttu-id="d31f7-143">To copy data from Drill, set the source type in the copy activity to **DrillSource**.</span><span class="sxs-lookup"><span data-stu-id="d31f7-143">To copy data from Drill, set the source type in the copy activity to **DrillSource**.</span></span> <span data-ttu-id="d31f7-144">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="d31f7-144">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="d31f7-145">Property</span><span class="sxs-lookup"><span data-stu-id="d31f7-145">Property</span></span> | <span data-ttu-id="d31f7-146">Description</span><span class="sxs-lookup"><span data-stu-id="d31f7-146">Description</span></span> | <span data-ttu-id="d31f7-147">Required</span><span class="sxs-lookup"><span data-stu-id="d31f7-147">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d31f7-148">type</span><span class="sxs-lookup"><span data-stu-id="d31f7-148">type</span></span> | <span data-ttu-id="d31f7-149">The type property of the copy activity source must be set to: **DrillSource**</span><span class="sxs-lookup"><span data-stu-id="d31f7-149">The type property of the copy activity source must be set to: **DrillSource**</span></span> | <span data-ttu-id="d31f7-150">Yes</span><span class="sxs-lookup"><span data-stu-id="d31f7-150">Yes</span></span> |
| <span data-ttu-id="d31f7-151">query</span><span class="sxs-lookup"><span data-stu-id="d31f7-151">query</span></span> | <span data-ttu-id="d31f7-152">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="d31f7-152">Use the custom SQL query to read data.</span></span> <span data-ttu-id="d31f7-153">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="d31f7-153">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="d31f7-154">Yes</span><span class="sxs-lookup"><span data-stu-id="d31f7-154">Yes</span></span> |

<span data-ttu-id="d31f7-155">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d31f7-155">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromDrill",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Drill input dataset name>",
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
                "type": "DrillSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="d31f7-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="d31f7-156">Next steps</span></span>
<span data-ttu-id="d31f7-157">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d31f7-157">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
