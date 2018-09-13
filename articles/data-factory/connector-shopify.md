---
title: Copy data from Shopify using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Shopify to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 21065950a886248dcf3cdbc795d0b77f74eaf808
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869052"
---
# <a name="copy-data-from-shopify-using-azure-data-factory"></a><span data-ttu-id="41738-103">Copy data from Shopify using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="41738-103">Copy data from Shopify using Azure Data Factory</span></span>

<span data-ttu-id="41738-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Shopify.</span><span class="sxs-lookup"><span data-stu-id="41738-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Shopify.</span></span> <span data-ttu-id="41738-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="41738-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41738-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="41738-106">This connector is currently in preview.</span></span> <span data-ttu-id="41738-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="41738-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="41738-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="41738-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="41738-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="41738-109">Supported capabilities</span></span>

<span data-ttu-id="41738-110">You can copy data from Shopify to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="41738-110">You can copy data from Shopify to any supported sink data store.</span></span> <span data-ttu-id="41738-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="41738-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="41738-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="41738-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="41738-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="41738-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="41738-114">The following sections provide details about properties that are used to define Data Factory entities specific to Shopify connector.</span><span class="sxs-lookup"><span data-stu-id="41738-114">The following sections provide details about properties that are used to define Data Factory entities specific to Shopify connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="41738-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="41738-115">Linked service properties</span></span>

<span data-ttu-id="41738-116">The following properties are supported for Shopify linked service:</span><span class="sxs-lookup"><span data-stu-id="41738-116">The following properties are supported for Shopify linked service:</span></span>

| <span data-ttu-id="41738-117">Property</span><span class="sxs-lookup"><span data-stu-id="41738-117">Property</span></span> | <span data-ttu-id="41738-118">Description</span><span class="sxs-lookup"><span data-stu-id="41738-118">Description</span></span> | <span data-ttu-id="41738-119">Required</span><span class="sxs-lookup"><span data-stu-id="41738-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="41738-120">type</span><span class="sxs-lookup"><span data-stu-id="41738-120">type</span></span> | <span data-ttu-id="41738-121">The type property must be set to: **Shopify**</span><span class="sxs-lookup"><span data-stu-id="41738-121">The type property must be set to: **Shopify**</span></span> | <span data-ttu-id="41738-122">Yes</span><span class="sxs-lookup"><span data-stu-id="41738-122">Yes</span></span> |
| <span data-ttu-id="41738-123">host</span><span class="sxs-lookup"><span data-stu-id="41738-123">host</span></span> | <span data-ttu-id="41738-124">The endpoint of the Shopify server.</span><span class="sxs-lookup"><span data-stu-id="41738-124">The endpoint of the Shopify server.</span></span> <span data-ttu-id="41738-125">(that is, mystore.myshopify.com)</span><span class="sxs-lookup"><span data-stu-id="41738-125">(that is, mystore.myshopify.com)</span></span>  | <span data-ttu-id="41738-126">Yes</span><span class="sxs-lookup"><span data-stu-id="41738-126">Yes</span></span> |
| <span data-ttu-id="41738-127">accessToken</span><span class="sxs-lookup"><span data-stu-id="41738-127">accessToken</span></span> | <span data-ttu-id="41738-128">The API access token that can be used to access Shopify’s data.</span><span class="sxs-lookup"><span data-stu-id="41738-128">The API access token that can be used to access Shopify’s data.</span></span> <span data-ttu-id="41738-129">The token does not expire if it is offline mode.</span><span class="sxs-lookup"><span data-stu-id="41738-129">The token does not expire if it is offline mode.</span></span> <span data-ttu-id="41738-130">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="41738-130">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="41738-131">Yes</span><span class="sxs-lookup"><span data-stu-id="41738-131">Yes</span></span> |
| <span data-ttu-id="41738-132">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="41738-132">useEncryptedEndpoints</span></span> | <span data-ttu-id="41738-133">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="41738-133">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="41738-134">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="41738-134">The default value is true.</span></span>  | <span data-ttu-id="41738-135">No</span><span class="sxs-lookup"><span data-stu-id="41738-135">No</span></span> |
| <span data-ttu-id="41738-136">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="41738-136">useHostVerification</span></span> | <span data-ttu-id="41738-137">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="41738-137">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="41738-138">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="41738-138">The default value is true.</span></span>  | <span data-ttu-id="41738-139">No</span><span class="sxs-lookup"><span data-stu-id="41738-139">No</span></span> |
| <span data-ttu-id="41738-140">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="41738-140">usePeerVerification</span></span> | <span data-ttu-id="41738-141">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="41738-141">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="41738-142">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="41738-142">The default value is true.</span></span>  | <span data-ttu-id="41738-143">No</span><span class="sxs-lookup"><span data-stu-id="41738-143">No</span></span> |

<span data-ttu-id="41738-144">**Example:**</span><span class="sxs-lookup"><span data-stu-id="41738-144">**Example:**</span></span>

```json
{
    "name": "ShopifyLinkedService",
    "properties": {
        "type": "Shopify",
        "typeProperties": {
            "host" : "mystore.myshopify.com",
            "accessToken": {
                 "type": "SecureString",
                 "value": "<accessToken>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="41738-145">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="41738-145">Dataset properties</span></span>

<span data-ttu-id="41738-146">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="41738-146">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="41738-147">This section provides a list of properties supported by Shopify dataset.</span><span class="sxs-lookup"><span data-stu-id="41738-147">This section provides a list of properties supported by Shopify dataset.</span></span>

<span data-ttu-id="41738-148">To copy data from Shopify, set the type property of the dataset to **ShopifyObject**.</span><span class="sxs-lookup"><span data-stu-id="41738-148">To copy data from Shopify, set the type property of the dataset to **ShopifyObject**.</span></span> <span data-ttu-id="41738-149">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="41738-149">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="41738-150">**Example**</span><span class="sxs-lookup"><span data-stu-id="41738-150">**Example**</span></span>

```json
{
    "name": "ShopifyDataset",
    "properties": {
        "type": "ShopifyObject",
        "linkedServiceName": {
            "referenceName": "<Shopify linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="41738-151">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="41738-151">Copy activity properties</span></span>

<span data-ttu-id="41738-152">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="41738-152">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="41738-153">This section provides a list of properties supported by Shopify source.</span><span class="sxs-lookup"><span data-stu-id="41738-153">This section provides a list of properties supported by Shopify source.</span></span>

### <a name="shopifysource-as-source"></a><span data-ttu-id="41738-154">ShopifySource as source</span><span class="sxs-lookup"><span data-stu-id="41738-154">ShopifySource as source</span></span>

<span data-ttu-id="41738-155">To copy data from Shopify, set the source type in the copy activity to **ShopifySource**.</span><span class="sxs-lookup"><span data-stu-id="41738-155">To copy data from Shopify, set the source type in the copy activity to **ShopifySource**.</span></span> <span data-ttu-id="41738-156">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="41738-156">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="41738-157">Property</span><span class="sxs-lookup"><span data-stu-id="41738-157">Property</span></span> | <span data-ttu-id="41738-158">Description</span><span class="sxs-lookup"><span data-stu-id="41738-158">Description</span></span> | <span data-ttu-id="41738-159">Required</span><span class="sxs-lookup"><span data-stu-id="41738-159">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="41738-160">type</span><span class="sxs-lookup"><span data-stu-id="41738-160">type</span></span> | <span data-ttu-id="41738-161">The type property of the copy activity source must be set to: **ShopifySource**</span><span class="sxs-lookup"><span data-stu-id="41738-161">The type property of the copy activity source must be set to: **ShopifySource**</span></span> | <span data-ttu-id="41738-162">Yes</span><span class="sxs-lookup"><span data-stu-id="41738-162">Yes</span></span> |
| <span data-ttu-id="41738-163">query</span><span class="sxs-lookup"><span data-stu-id="41738-163">query</span></span> | <span data-ttu-id="41738-164">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="41738-164">Use the custom SQL query to read data.</span></span> <span data-ttu-id="41738-165">For example: `"SELECT * FROM "Products" WHERE Product_Id = '123'"`.</span><span class="sxs-lookup"><span data-stu-id="41738-165">For example: `"SELECT * FROM "Products" WHERE Product_Id = '123'"`.</span></span> | <span data-ttu-id="41738-166">Yes</span><span class="sxs-lookup"><span data-stu-id="41738-166">Yes</span></span> |

<span data-ttu-id="41738-167">**Example:**</span><span class="sxs-lookup"><span data-stu-id="41738-167">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromShopify",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Shopify input dataset name>",
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
                "type": "ShopifySource",
                "query": "SELECT * FROM \"Products\" WHERE Product_Id = '123'"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="41738-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="41738-168">Next steps</span></span>
<span data-ttu-id="41738-169">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="41738-169">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
