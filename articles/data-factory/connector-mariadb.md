---
title: Copy data from MariaDB using Azure Data Factory  | Microsoft Docs
description: Learn how to copy data from MariaDB to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 93d4886d5c266555a5c61a121622943f218caa48
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965929"
---
# <a name="copy-data-from-mariadb-using-azure-data-factory"></a><span data-ttu-id="fa189-103">Copy data from MariaDB using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="fa189-103">Copy data from MariaDB using Azure Data Factory</span></span> 

<span data-ttu-id="fa189-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from MariaDB.</span><span class="sxs-lookup"><span data-stu-id="fa189-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from MariaDB.</span></span> <span data-ttu-id="fa189-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="fa189-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="fa189-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="fa189-106">Supported capabilities</span></span>

<span data-ttu-id="fa189-107">You can copy data from MariaDB to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="fa189-107">You can copy data from MariaDB to any supported sink data store.</span></span> <span data-ttu-id="fa189-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="fa189-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="fa189-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="fa189-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

<span data-ttu-id="fa189-110">This connector currently supports MariaDB of version less than 10.2.</span><span class="sxs-lookup"><span data-stu-id="fa189-110">This connector currently supports MariaDB of version less than 10.2.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fa189-111">Getting started</span><span class="sxs-lookup"><span data-stu-id="fa189-111">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="fa189-112">The following sections provide details about properties that are used to define Data Factory entities specific to MariaDB connector.</span><span class="sxs-lookup"><span data-stu-id="fa189-112">The following sections provide details about properties that are used to define Data Factory entities specific to MariaDB connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fa189-113">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="fa189-113">Linked service properties</span></span>

<span data-ttu-id="fa189-114">The following properties are supported for MariaDB linked service:</span><span class="sxs-lookup"><span data-stu-id="fa189-114">The following properties are supported for MariaDB linked service:</span></span>

| <span data-ttu-id="fa189-115">Property</span><span class="sxs-lookup"><span data-stu-id="fa189-115">Property</span></span> | <span data-ttu-id="fa189-116">Description</span><span class="sxs-lookup"><span data-stu-id="fa189-116">Description</span></span> | <span data-ttu-id="fa189-117">Required</span><span class="sxs-lookup"><span data-stu-id="fa189-117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fa189-118">type</span><span class="sxs-lookup"><span data-stu-id="fa189-118">type</span></span> | <span data-ttu-id="fa189-119">The type property must be set to: **MariaDB**</span><span class="sxs-lookup"><span data-stu-id="fa189-119">The type property must be set to: **MariaDB**</span></span> | <span data-ttu-id="fa189-120">Yes</span><span class="sxs-lookup"><span data-stu-id="fa189-120">Yes</span></span> |
| <span data-ttu-id="fa189-121">connectionString</span><span class="sxs-lookup"><span data-stu-id="fa189-121">connectionString</span></span> | <span data-ttu-id="fa189-122">An ODBC connection string to connect to MariaDB.</span><span class="sxs-lookup"><span data-stu-id="fa189-122">An ODBC connection string to connect to MariaDB.</span></span> <span data-ttu-id="fa189-123">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="fa189-123">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="fa189-124">Yes</span><span class="sxs-lookup"><span data-stu-id="fa189-124">Yes</span></span> |
| <span data-ttu-id="fa189-125">connectVia</span><span class="sxs-lookup"><span data-stu-id="fa189-125">connectVia</span></span> | <span data-ttu-id="fa189-126">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="fa189-126">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="fa189-127">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="fa189-127">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="fa189-128">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="fa189-128">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="fa189-129">No</span><span class="sxs-lookup"><span data-stu-id="fa189-129">No</span></span> |

<span data-ttu-id="fa189-130">**Example:**</span><span class="sxs-lookup"><span data-stu-id="fa189-130">**Example:**</span></span>

```json
{
    "name": "MariaDBLinkedService",
    "properties": {
        "type": "MariaDB",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<host>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="fa189-131">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="fa189-131">Dataset properties</span></span>

<span data-ttu-id="fa189-132">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="fa189-132">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="fa189-133">This section provides a list of properties supported by MariaDB dataset.</span><span class="sxs-lookup"><span data-stu-id="fa189-133">This section provides a list of properties supported by MariaDB dataset.</span></span>

<span data-ttu-id="fa189-134">To copy data from MariaDB, set the type property of the dataset to **MariaDBTable**.</span><span class="sxs-lookup"><span data-stu-id="fa189-134">To copy data from MariaDB, set the type property of the dataset to **MariaDBTable**.</span></span> <span data-ttu-id="fa189-135">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="fa189-135">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="fa189-136">**Example**</span><span class="sxs-lookup"><span data-stu-id="fa189-136">**Example**</span></span>

```json
{
    "name": "MariaDBDataset",
    "properties": {
        "type": "MariaDBTable",
        "linkedServiceName": {
            "referenceName": "<MariaDB linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="fa189-137">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="fa189-137">Copy activity properties</span></span>

<span data-ttu-id="fa189-138">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="fa189-138">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="fa189-139">This section provides a list of properties supported by MariaDB source.</span><span class="sxs-lookup"><span data-stu-id="fa189-139">This section provides a list of properties supported by MariaDB source.</span></span>

### <a name="mariadbsource-as-source"></a><span data-ttu-id="fa189-140">MariaDBSource as source</span><span class="sxs-lookup"><span data-stu-id="fa189-140">MariaDBSource as source</span></span>

<span data-ttu-id="fa189-141">To copy data from MariaDB, set the source type in the copy activity to **MariaDBSource**.</span><span class="sxs-lookup"><span data-stu-id="fa189-141">To copy data from MariaDB, set the source type in the copy activity to **MariaDBSource**.</span></span> <span data-ttu-id="fa189-142">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="fa189-142">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="fa189-143">Property</span><span class="sxs-lookup"><span data-stu-id="fa189-143">Property</span></span> | <span data-ttu-id="fa189-144">Description</span><span class="sxs-lookup"><span data-stu-id="fa189-144">Description</span></span> | <span data-ttu-id="fa189-145">Required</span><span class="sxs-lookup"><span data-stu-id="fa189-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fa189-146">type</span><span class="sxs-lookup"><span data-stu-id="fa189-146">type</span></span> | <span data-ttu-id="fa189-147">The type property of the copy activity source must be set to: **MariaDBSource**</span><span class="sxs-lookup"><span data-stu-id="fa189-147">The type property of the copy activity source must be set to: **MariaDBSource**</span></span> | <span data-ttu-id="fa189-148">Yes</span><span class="sxs-lookup"><span data-stu-id="fa189-148">Yes</span></span> |
| <span data-ttu-id="fa189-149">query</span><span class="sxs-lookup"><span data-stu-id="fa189-149">query</span></span> | <span data-ttu-id="fa189-150">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="fa189-150">Use the custom SQL query to read data.</span></span> <span data-ttu-id="fa189-151">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="fa189-151">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="fa189-152">Yes</span><span class="sxs-lookup"><span data-stu-id="fa189-152">Yes</span></span> |

<span data-ttu-id="fa189-153">**Example:**</span><span class="sxs-lookup"><span data-stu-id="fa189-153">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromMariaDB",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<MariaDB input dataset name>",
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
                "type": "MariaDBSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="fa189-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa189-154">Next steps</span></span>
<span data-ttu-id="fa189-155">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="fa189-155">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
