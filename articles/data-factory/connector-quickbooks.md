---
title: Copy data from QuickBooks using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from QuickBooks to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 4e73b444335fe0e96ff453570ee0092f38ab9a4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867019"
---
# <a name="copy-data-from-quickbooks-using-azure-data-factory"></a><span data-ttu-id="458a2-103">Copy data from QuickBooks using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="458a2-103">Copy data from QuickBooks using Azure Data Factory</span></span>

<span data-ttu-id="458a2-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="458a2-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from QuickBooks.</span></span> <span data-ttu-id="458a2-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="458a2-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="458a2-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="458a2-106">This connector is currently in preview.</span></span> <span data-ttu-id="458a2-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="458a2-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="458a2-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="458a2-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="458a2-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="458a2-109">Supported capabilities</span></span>

<span data-ttu-id="458a2-110">You can copy data from QuickBooks to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="458a2-110">You can copy data from QuickBooks to any supported sink data store.</span></span> <span data-ttu-id="458a2-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="458a2-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="458a2-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="458a2-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

<span data-ttu-id="458a2-113">Currently this connector only support 1.0a, which means you need to have a developer account with apps created before July 17, 2017.</span><span class="sxs-lookup"><span data-stu-id="458a2-113">Currently this connector only support 1.0a, which means you need to have a developer account with apps created before July 17, 2017.</span></span>

## <a name="getting-started"></a><span data-ttu-id="458a2-114">Getting started</span><span class="sxs-lookup"><span data-stu-id="458a2-114">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="458a2-115">The following sections provide details about properties that are used to define Data Factory entities specific to QuickBooks connector.</span><span class="sxs-lookup"><span data-stu-id="458a2-115">The following sections provide details about properties that are used to define Data Factory entities specific to QuickBooks connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="458a2-116">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="458a2-116">Linked service properties</span></span>

<span data-ttu-id="458a2-117">The following properties are supported for QuickBooks linked service:</span><span class="sxs-lookup"><span data-stu-id="458a2-117">The following properties are supported for QuickBooks linked service:</span></span>

| <span data-ttu-id="458a2-118">Property</span><span class="sxs-lookup"><span data-stu-id="458a2-118">Property</span></span> | <span data-ttu-id="458a2-119">Description</span><span class="sxs-lookup"><span data-stu-id="458a2-119">Description</span></span> | <span data-ttu-id="458a2-120">Required</span><span class="sxs-lookup"><span data-stu-id="458a2-120">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="458a2-121">type</span><span class="sxs-lookup"><span data-stu-id="458a2-121">type</span></span> | <span data-ttu-id="458a2-122">The type property must be set to: **QuickBooks**</span><span class="sxs-lookup"><span data-stu-id="458a2-122">The type property must be set to: **QuickBooks**</span></span> | <span data-ttu-id="458a2-123">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-123">Yes</span></span> |
| <span data-ttu-id="458a2-124">endpoint</span><span class="sxs-lookup"><span data-stu-id="458a2-124">endpoint</span></span> | <span data-ttu-id="458a2-125">The endpoint of the QuickBooks server.</span><span class="sxs-lookup"><span data-stu-id="458a2-125">The endpoint of the QuickBooks server.</span></span> <span data-ttu-id="458a2-126">(that is, quickbooks.api.intuit.com)</span><span class="sxs-lookup"><span data-stu-id="458a2-126">(that is, quickbooks.api.intuit.com)</span></span>  | <span data-ttu-id="458a2-127">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-127">Yes</span></span> |
| <span data-ttu-id="458a2-128">companyId</span><span class="sxs-lookup"><span data-stu-id="458a2-128">companyId</span></span> | <span data-ttu-id="458a2-129">The company ID of the QuickBooks company to authorize.</span><span class="sxs-lookup"><span data-stu-id="458a2-129">The company ID of the QuickBooks company to authorize.</span></span>  | <span data-ttu-id="458a2-130">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-130">Yes</span></span> |
| <span data-ttu-id="458a2-131">consumerKey</span><span class="sxs-lookup"><span data-stu-id="458a2-131">consumerKey</span></span> | <span data-ttu-id="458a2-132">The consumer key for OAuth 1.0 authentication.</span><span class="sxs-lookup"><span data-stu-id="458a2-132">The consumer key for OAuth 1.0 authentication.</span></span> | <span data-ttu-id="458a2-133">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-133">Yes</span></span> |
| <span data-ttu-id="458a2-134">consumerSecret</span><span class="sxs-lookup"><span data-stu-id="458a2-134">consumerSecret</span></span> | <span data-ttu-id="458a2-135">The consumer secret for OAuth 1.0 authentication.</span><span class="sxs-lookup"><span data-stu-id="458a2-135">The consumer secret for OAuth 1.0 authentication.</span></span> <span data-ttu-id="458a2-136">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="458a2-136">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="458a2-137">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-137">Yes</span></span> |
| <span data-ttu-id="458a2-138">accessToken</span><span class="sxs-lookup"><span data-stu-id="458a2-138">accessToken</span></span> | <span data-ttu-id="458a2-139">The access token for OAuth 1.0 authentication.</span><span class="sxs-lookup"><span data-stu-id="458a2-139">The access token for OAuth 1.0 authentication.</span></span> <span data-ttu-id="458a2-140">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="458a2-140">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="458a2-141">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-141">Yes</span></span> |
| <span data-ttu-id="458a2-142">accessTokenSecret</span><span class="sxs-lookup"><span data-stu-id="458a2-142">accessTokenSecret</span></span> | <span data-ttu-id="458a2-143">The access token secret for OAuth 1.0 authentication.</span><span class="sxs-lookup"><span data-stu-id="458a2-143">The access token secret for OAuth 1.0 authentication.</span></span> <span data-ttu-id="458a2-144">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="458a2-144">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="458a2-145">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-145">Yes</span></span> |
| <span data-ttu-id="458a2-146">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="458a2-146">useEncryptedEndpoints</span></span> | <span data-ttu-id="458a2-147">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="458a2-147">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="458a2-148">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="458a2-148">The default value is true.</span></span>  | <span data-ttu-id="458a2-149">No</span><span class="sxs-lookup"><span data-stu-id="458a2-149">No</span></span> |

<span data-ttu-id="458a2-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="458a2-150">**Example:**</span></span>

```json
{
    "name": "QuickBooksLinkedService",
    "properties": {
        "type": "QuickBooks",
        "typeProperties": {
            "endpoint" : "quickbooks.api.intuit.com",
            "companyId" : "<companyId>",
            "consumerKey": "<consumerKey>",
            "consumerSecret": {
                "type": "SecureString",
                "value": "<consumerSecret>"
            },
            "accessToken": {
                 "type": "SecureString",
                 "value": "<accessToken>"
            },
            "accessTokenSecret": {
                 "type": "SecureString",
                 "value": "<accessTokenSecret>"
            },
            "useEncryptedEndpoints" : true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="458a2-151">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="458a2-151">Dataset properties</span></span>

<span data-ttu-id="458a2-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="458a2-152">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="458a2-153">This section provides a list of properties supported by QuickBooks dataset.</span><span class="sxs-lookup"><span data-stu-id="458a2-153">This section provides a list of properties supported by QuickBooks dataset.</span></span>

<span data-ttu-id="458a2-154">To copy data from QuickBooks, set the type property of the dataset to **QuickBooksObject**.</span><span class="sxs-lookup"><span data-stu-id="458a2-154">To copy data from QuickBooks, set the type property of the dataset to **QuickBooksObject**.</span></span> <span data-ttu-id="458a2-155">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="458a2-155">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="458a2-156">**Example**</span><span class="sxs-lookup"><span data-stu-id="458a2-156">**Example**</span></span>

```json
{
    "name": "QuickBooksDataset",
    "properties": {
        "type": "QuickBooksObject",
        "linkedServiceName": {
            "referenceName": "<QuickBooks linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="458a2-157">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="458a2-157">Copy activity properties</span></span>

<span data-ttu-id="458a2-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="458a2-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="458a2-159">This section provides a list of properties supported by QuickBooks source.</span><span class="sxs-lookup"><span data-stu-id="458a2-159">This section provides a list of properties supported by QuickBooks source.</span></span>

### <a name="quickbookssource-as-source"></a><span data-ttu-id="458a2-160">QuickBooksSource as source</span><span class="sxs-lookup"><span data-stu-id="458a2-160">QuickBooksSource as source</span></span>

<span data-ttu-id="458a2-161">To copy data from QuickBooks, set the source type in the copy activity to **QuickBooksSource**.</span><span class="sxs-lookup"><span data-stu-id="458a2-161">To copy data from QuickBooks, set the source type in the copy activity to **QuickBooksSource**.</span></span> <span data-ttu-id="458a2-162">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="458a2-162">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="458a2-163">Property</span><span class="sxs-lookup"><span data-stu-id="458a2-163">Property</span></span> | <span data-ttu-id="458a2-164">Description</span><span class="sxs-lookup"><span data-stu-id="458a2-164">Description</span></span> | <span data-ttu-id="458a2-165">Required</span><span class="sxs-lookup"><span data-stu-id="458a2-165">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="458a2-166">type</span><span class="sxs-lookup"><span data-stu-id="458a2-166">type</span></span> | <span data-ttu-id="458a2-167">The type property of the copy activity source must be set to: **QuickBooksSource**</span><span class="sxs-lookup"><span data-stu-id="458a2-167">The type property of the copy activity source must be set to: **QuickBooksSource**</span></span> | <span data-ttu-id="458a2-168">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-168">Yes</span></span> |
| <span data-ttu-id="458a2-169">query</span><span class="sxs-lookup"><span data-stu-id="458a2-169">query</span></span> | <span data-ttu-id="458a2-170">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="458a2-170">Use the custom SQL query to read data.</span></span> <span data-ttu-id="458a2-171">For example: `"SELECT * FROM "Bill" WHERE Id = '123'"`.</span><span class="sxs-lookup"><span data-stu-id="458a2-171">For example: `"SELECT * FROM "Bill" WHERE Id = '123'"`.</span></span> | <span data-ttu-id="458a2-172">Yes</span><span class="sxs-lookup"><span data-stu-id="458a2-172">Yes</span></span> |

<span data-ttu-id="458a2-173">**Example:**</span><span class="sxs-lookup"><span data-stu-id="458a2-173">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromQuickBooks",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<QuickBooks input dataset name>",
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
                "type": "QuickBooksSource",
                "query": "SELECT * FROM \"Bill\" WHERE Id = '123' "
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="458a2-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="458a2-174">Next steps</span></span>
<span data-ttu-id="458a2-175">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="458a2-175">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
