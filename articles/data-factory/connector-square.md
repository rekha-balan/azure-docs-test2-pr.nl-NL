---
title: Copy data from Square using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Square to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 390dbb35faec45e8629c2d870f2463bb3965a88b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869574"
---
# <a name="copy-data-from-square-using-azure-data-factory"></a><span data-ttu-id="7b7a4-103">Copy data from Square using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7b7a4-103">Copy data from Square using Azure Data Factory</span></span>

<span data-ttu-id="7b7a4-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Square.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Square.</span></span> <span data-ttu-id="7b7a4-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b7a4-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-106">This connector is currently in preview.</span></span> <span data-ttu-id="7b7a4-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="7b7a4-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="7b7a4-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="7b7a4-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="7b7a4-109">Supported capabilities</span></span>

<span data-ttu-id="7b7a4-110">You can copy data from Square to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-110">You can copy data from Square to any supported sink data store.</span></span> <span data-ttu-id="7b7a4-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="7b7a4-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7b7a4-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="7b7a4-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="7b7a4-114">The following sections provide details about properties that are used to define Data Factory entities specific to Square connector.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-114">The following sections provide details about properties that are used to define Data Factory entities specific to Square connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7b7a4-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="7b7a4-115">Linked service properties</span></span>

<span data-ttu-id="7b7a4-116">The following properties are supported for Square linked service:</span><span class="sxs-lookup"><span data-stu-id="7b7a4-116">The following properties are supported for Square linked service:</span></span>

| <span data-ttu-id="7b7a4-117">Property</span><span class="sxs-lookup"><span data-stu-id="7b7a4-117">Property</span></span> | <span data-ttu-id="7b7a4-118">Description</span><span class="sxs-lookup"><span data-stu-id="7b7a4-118">Description</span></span> | <span data-ttu-id="7b7a4-119">Required</span><span class="sxs-lookup"><span data-stu-id="7b7a4-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7b7a4-120">type</span><span class="sxs-lookup"><span data-stu-id="7b7a4-120">type</span></span> | <span data-ttu-id="7b7a4-121">The type property must be set to: **Square**</span><span class="sxs-lookup"><span data-stu-id="7b7a4-121">The type property must be set to: **Square**</span></span> | <span data-ttu-id="7b7a4-122">Yes</span><span class="sxs-lookup"><span data-stu-id="7b7a4-122">Yes</span></span> |
| <span data-ttu-id="7b7a4-123">host</span><span class="sxs-lookup"><span data-stu-id="7b7a4-123">host</span></span> | <span data-ttu-id="7b7a4-124">The URL of the Square instance.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-124">The URL of the Square instance.</span></span> <span data-ttu-id="7b7a4-125">(i.e. mystore.mysquare.com)</span><span class="sxs-lookup"><span data-stu-id="7b7a4-125">(i.e. mystore.mysquare.com)</span></span>  | <span data-ttu-id="7b7a4-126">Yes</span><span class="sxs-lookup"><span data-stu-id="7b7a4-126">Yes</span></span> |
| <span data-ttu-id="7b7a4-127">clientId</span><span class="sxs-lookup"><span data-stu-id="7b7a4-127">clientId</span></span> | <span data-ttu-id="7b7a4-128">The client ID associated with your Square application.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-128">The client ID associated with your Square application.</span></span>  | <span data-ttu-id="7b7a4-129">Yes</span><span class="sxs-lookup"><span data-stu-id="7b7a4-129">Yes</span></span> |
| <span data-ttu-id="7b7a4-130">clientSecret</span><span class="sxs-lookup"><span data-stu-id="7b7a4-130">clientSecret</span></span> | <span data-ttu-id="7b7a4-131">The client secret associated with your Square application.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-131">The client secret associated with your Square application.</span></span> <span data-ttu-id="7b7a4-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="7b7a4-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="7b7a4-133">Yes</span><span class="sxs-lookup"><span data-stu-id="7b7a4-133">Yes</span></span> |
| <span data-ttu-id="7b7a4-134">redirectUri</span><span class="sxs-lookup"><span data-stu-id="7b7a4-134">redirectUri</span></span> | <span data-ttu-id="7b7a4-135">The redirect URL assigned in the Square application dashboard.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-135">The redirect URL assigned in the Square application dashboard.</span></span> <span data-ttu-id="7b7a4-136">(i.e. http://localhost:2500)</span><span class="sxs-lookup"><span data-stu-id="7b7a4-136">(i.e. http://localhost:2500)</span></span>  | <span data-ttu-id="7b7a4-137">Yes</span><span class="sxs-lookup"><span data-stu-id="7b7a4-137">Yes</span></span> |
| <span data-ttu-id="7b7a4-138">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="7b7a4-138">useEncryptedEndpoints</span></span> | <span data-ttu-id="7b7a4-139">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-139">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="7b7a4-140">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-140">The default value is true.</span></span>  | <span data-ttu-id="7b7a4-141">No</span><span class="sxs-lookup"><span data-stu-id="7b7a4-141">No</span></span> |
| <span data-ttu-id="7b7a4-142">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="7b7a4-142">useHostVerification</span></span> | <span data-ttu-id="7b7a4-143">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-143">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="7b7a4-144">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-144">The default value is true.</span></span>  | <span data-ttu-id="7b7a4-145">No</span><span class="sxs-lookup"><span data-stu-id="7b7a4-145">No</span></span> |
| <span data-ttu-id="7b7a4-146">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="7b7a4-146">usePeerVerification</span></span> | <span data-ttu-id="7b7a4-147">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-147">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="7b7a4-148">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-148">The default value is true.</span></span>  | <span data-ttu-id="7b7a4-149">No</span><span class="sxs-lookup"><span data-stu-id="7b7a4-149">No</span></span> |

<span data-ttu-id="7b7a4-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="7b7a4-150">**Example:**</span></span>

```json
{
    "name": "SquareLinkedService",
    "properties": {
        "type": "Square",
        "typeProperties": {
            "host" : "mystore.mysquare.com",
            "clientId" : "<clientId>",
            "clientSecret": {
                 "type": "SecureString",
                 "value": "<clientSecret>"
            },
            "redirectUri" : "http://localhost:2500"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="7b7a4-151">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="7b7a4-151">Dataset properties</span></span>

<span data-ttu-id="7b7a4-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="7b7a4-153">This section provides a list of properties supported by Square dataset.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-153">This section provides a list of properties supported by Square dataset.</span></span>

<span data-ttu-id="7b7a4-154">To copy data from Square, set the type property of the dataset to **SquareObject**.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-154">To copy data from Square, set the type property of the dataset to **SquareObject**.</span></span> <span data-ttu-id="7b7a4-155">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-155">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="7b7a4-156">**Example**</span><span class="sxs-lookup"><span data-stu-id="7b7a4-156">**Example**</span></span>

```json
{
    "name": "SquareDataset",
    "properties": {
        "type": "SquareObject",
        "linkedServiceName": {
            "referenceName": "<Square linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="7b7a4-157">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="7b7a4-157">Copy activity properties</span></span>

<span data-ttu-id="7b7a4-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="7b7a4-159">This section provides a list of properties supported by Square source.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-159">This section provides a list of properties supported by Square source.</span></span>

### <a name="squaresource-as-source"></a><span data-ttu-id="7b7a4-160">SquareSource as source</span><span class="sxs-lookup"><span data-stu-id="7b7a4-160">SquareSource as source</span></span>

<span data-ttu-id="7b7a4-161">To copy data from Square, set the source type in the copy activity to **SquareSource**.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-161">To copy data from Square, set the source type in the copy activity to **SquareSource**.</span></span> <span data-ttu-id="7b7a4-162">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="7b7a4-162">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="7b7a4-163">Property</span><span class="sxs-lookup"><span data-stu-id="7b7a4-163">Property</span></span> | <span data-ttu-id="7b7a4-164">Description</span><span class="sxs-lookup"><span data-stu-id="7b7a4-164">Description</span></span> | <span data-ttu-id="7b7a4-165">Required</span><span class="sxs-lookup"><span data-stu-id="7b7a4-165">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7b7a4-166">type</span><span class="sxs-lookup"><span data-stu-id="7b7a4-166">type</span></span> | <span data-ttu-id="7b7a4-167">The type property of the copy activity source must be set to: **SquareSource**</span><span class="sxs-lookup"><span data-stu-id="7b7a4-167">The type property of the copy activity source must be set to: **SquareSource**</span></span> | <span data-ttu-id="7b7a4-168">Yes</span><span class="sxs-lookup"><span data-stu-id="7b7a4-168">Yes</span></span> |
| <span data-ttu-id="7b7a4-169">query</span><span class="sxs-lookup"><span data-stu-id="7b7a4-169">query</span></span> | <span data-ttu-id="7b7a4-170">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-170">Use the custom SQL query to read data.</span></span> <span data-ttu-id="7b7a4-171">For example: `"SELECT * FROM Business"`.</span><span class="sxs-lookup"><span data-stu-id="7b7a4-171">For example: `"SELECT * FROM Business"`.</span></span> | <span data-ttu-id="7b7a4-172">Yes</span><span class="sxs-lookup"><span data-stu-id="7b7a4-172">Yes</span></span> |

<span data-ttu-id="7b7a4-173">**Example:**</span><span class="sxs-lookup"><span data-stu-id="7b7a4-173">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSquare",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Square input dataset name>",
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
                "type": "SquareSource",
                "query": "SELECT * FROM Business"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="7b7a4-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b7a4-174">Next steps</span></span>
<span data-ttu-id="7b7a4-175">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7b7a4-175">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
