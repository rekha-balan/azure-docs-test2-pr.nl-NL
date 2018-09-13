---
title: Copy data from Amazon Marketplace Web Service using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Amazon Marketplace Web Service to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: c456f87b451c5876653d704ec367629c2856a1f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868285"
---
# <a name="copy-data-from-amazon-marketplace-web-service-using-azure-data-factory"></a><span data-ttu-id="09a18-103">Copy data from Amazon Marketplace Web Service using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="09a18-103">Copy data from Amazon Marketplace Web Service using Azure Data Factory</span></span>

<span data-ttu-id="09a18-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Amazon Marketplace Web Service.</span><span class="sxs-lookup"><span data-stu-id="09a18-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Amazon Marketplace Web Service.</span></span> <span data-ttu-id="09a18-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="09a18-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09a18-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="09a18-106">This connector is currently in preview.</span></span> <span data-ttu-id="09a18-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="09a18-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="09a18-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="09a18-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="09a18-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="09a18-109">Supported capabilities</span></span>

<span data-ttu-id="09a18-110">You can copy data from Amazon Marketplace Web Service to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="09a18-110">You can copy data from Amazon Marketplace Web Service to any supported sink data store.</span></span> <span data-ttu-id="09a18-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="09a18-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="09a18-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="09a18-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="09a18-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="09a18-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="09a18-114">The following sections provide details about properties that are used to define Data Factory entities specific to Amazon Marketplace Web Service connector.</span><span class="sxs-lookup"><span data-stu-id="09a18-114">The following sections provide details about properties that are used to define Data Factory entities specific to Amazon Marketplace Web Service connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="09a18-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="09a18-115">Linked service properties</span></span>

<span data-ttu-id="09a18-116">The following properties are supported for Amazon Marketplace Web Service linked service:</span><span class="sxs-lookup"><span data-stu-id="09a18-116">The following properties are supported for Amazon Marketplace Web Service linked service:</span></span>

| <span data-ttu-id="09a18-117">Property</span><span class="sxs-lookup"><span data-stu-id="09a18-117">Property</span></span> | <span data-ttu-id="09a18-118">Description</span><span class="sxs-lookup"><span data-stu-id="09a18-118">Description</span></span> | <span data-ttu-id="09a18-119">Required</span><span class="sxs-lookup"><span data-stu-id="09a18-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="09a18-120">type</span><span class="sxs-lookup"><span data-stu-id="09a18-120">type</span></span> | <span data-ttu-id="09a18-121">The type property must be set to: **AmazonMWS**</span><span class="sxs-lookup"><span data-stu-id="09a18-121">The type property must be set to: **AmazonMWS**</span></span> | <span data-ttu-id="09a18-122">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-122">Yes</span></span> |
| <span data-ttu-id="09a18-123">endpoint</span><span class="sxs-lookup"><span data-stu-id="09a18-123">endpoint</span></span> | <span data-ttu-id="09a18-124">The endpoint of the Amazon MWS server, (that is, mws.amazonservices.com)</span><span class="sxs-lookup"><span data-stu-id="09a18-124">The endpoint of the Amazon MWS server, (that is, mws.amazonservices.com)</span></span>  | <span data-ttu-id="09a18-125">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-125">Yes</span></span> |
| <span data-ttu-id="09a18-126">marketplaceID</span><span class="sxs-lookup"><span data-stu-id="09a18-126">marketplaceID</span></span> | <span data-ttu-id="09a18-127">The Amazon Marketplace ID you want to retrieve data from.</span><span class="sxs-lookup"><span data-stu-id="09a18-127">The Amazon Marketplace ID you want to retrieve data from.</span></span> <span data-ttu-id="09a18-128">To retrieve data from multiple Marketplace IDs, separate them with a comma (`,`).</span><span class="sxs-lookup"><span data-stu-id="09a18-128">To retrieve data from multiple Marketplace IDs, separate them with a comma (`,`).</span></span> <span data-ttu-id="09a18-129">(that is, A2EUQ1WTGCTBG2)</span><span class="sxs-lookup"><span data-stu-id="09a18-129">(that is, A2EUQ1WTGCTBG2)</span></span>  | <span data-ttu-id="09a18-130">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-130">Yes</span></span> |
| <span data-ttu-id="09a18-131">sellerID</span><span class="sxs-lookup"><span data-stu-id="09a18-131">sellerID</span></span> | <span data-ttu-id="09a18-132">The Amazon seller ID.</span><span class="sxs-lookup"><span data-stu-id="09a18-132">The Amazon seller ID.</span></span>  | <span data-ttu-id="09a18-133">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-133">Yes</span></span> |
| <span data-ttu-id="09a18-134">mwsAuthToken</span><span class="sxs-lookup"><span data-stu-id="09a18-134">mwsAuthToken</span></span> | <span data-ttu-id="09a18-135">The Amazon MWS authentication token.</span><span class="sxs-lookup"><span data-stu-id="09a18-135">The Amazon MWS authentication token.</span></span> <span data-ttu-id="09a18-136">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="09a18-136">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="09a18-137">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-137">Yes</span></span> |
| <span data-ttu-id="09a18-138">accessKeyId</span><span class="sxs-lookup"><span data-stu-id="09a18-138">accessKeyId</span></span> | <span data-ttu-id="09a18-139">The access key ID used to access data.</span><span class="sxs-lookup"><span data-stu-id="09a18-139">The access key ID used to access data.</span></span>  | <span data-ttu-id="09a18-140">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-140">Yes</span></span> |
| <span data-ttu-id="09a18-141">secretKey</span><span class="sxs-lookup"><span data-stu-id="09a18-141">secretKey</span></span> | <span data-ttu-id="09a18-142">The secret key used to access data.</span><span class="sxs-lookup"><span data-stu-id="09a18-142">The secret key used to access data.</span></span> <span data-ttu-id="09a18-143">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="09a18-143">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="09a18-144">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-144">Yes</span></span> |
| <span data-ttu-id="09a18-145">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="09a18-145">useEncryptedEndpoints</span></span> | <span data-ttu-id="09a18-146">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="09a18-146">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="09a18-147">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="09a18-147">The default value is true.</span></span>  | <span data-ttu-id="09a18-148">No</span><span class="sxs-lookup"><span data-stu-id="09a18-148">No</span></span> |
| <span data-ttu-id="09a18-149">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="09a18-149">useHostVerification</span></span> | <span data-ttu-id="09a18-150">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="09a18-150">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="09a18-151">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="09a18-151">The default value is true.</span></span>  | <span data-ttu-id="09a18-152">No</span><span class="sxs-lookup"><span data-stu-id="09a18-152">No</span></span> |
| <span data-ttu-id="09a18-153">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="09a18-153">usePeerVerification</span></span> | <span data-ttu-id="09a18-154">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="09a18-154">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="09a18-155">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="09a18-155">The default value is true.</span></span>  | <span data-ttu-id="09a18-156">No</span><span class="sxs-lookup"><span data-stu-id="09a18-156">No</span></span> |

<span data-ttu-id="09a18-157">**Example:**</span><span class="sxs-lookup"><span data-stu-id="09a18-157">**Example:**</span></span>

```json
{
    "name": "AmazonMWSLinkedService",
    "properties": {
        "type": "AmazonMWS",
        "typeProperties": {
            "endpoint" : "mws.amazonservices.com",
            "marketplaceID" : "A2EUQ1WTGCTBG2",
            "sellerID" : "<sellerID>",
            "mwsAuthToken": {
                 "type": "SecureString",
                 "value": "<mwsAuthToken>"
            },
            "accessKeyId" : "<accessKeyId>",
            "secretKey": {
                 "type": "SecureString",
                 "value": "<secretKey>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="09a18-158">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="09a18-158">Dataset properties</span></span>

<span data-ttu-id="09a18-159">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="09a18-159">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="09a18-160">This section provides a list of properties supported by Amazon Marketplace Web Service dataset.</span><span class="sxs-lookup"><span data-stu-id="09a18-160">This section provides a list of properties supported by Amazon Marketplace Web Service dataset.</span></span>

<span data-ttu-id="09a18-161">To copy data from Amazon Marketplace Web Service, set the type property of the dataset to **AmazonMWSObject**.</span><span class="sxs-lookup"><span data-stu-id="09a18-161">To copy data from Amazon Marketplace Web Service, set the type property of the dataset to **AmazonMWSObject**.</span></span> <span data-ttu-id="09a18-162">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="09a18-162">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="09a18-163">**Example**</span><span class="sxs-lookup"><span data-stu-id="09a18-163">**Example**</span></span>

```json
{
    "name": "AmazonMWSDataset",
    "properties": {
        "type": "AmazonMWSObject",
        "linkedServiceName": {
            "referenceName": "<AmazonMWS linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}

```

## <a name="copy-activity-properties"></a><span data-ttu-id="09a18-164">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="09a18-164">Copy activity properties</span></span>

<span data-ttu-id="09a18-165">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="09a18-165">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="09a18-166">This section provides a list of properties supported by Amazon Marketplace Web Service source.</span><span class="sxs-lookup"><span data-stu-id="09a18-166">This section provides a list of properties supported by Amazon Marketplace Web Service source.</span></span>

### <a name="amazonmwssource-as-source"></a><span data-ttu-id="09a18-167">AmazonMWSSource as source</span><span class="sxs-lookup"><span data-stu-id="09a18-167">AmazonMWSSource as source</span></span>

<span data-ttu-id="09a18-168">To copy data from Amazon Marketplace Web Service, set the source type in the copy activity to **AmazonMWSSource**.</span><span class="sxs-lookup"><span data-stu-id="09a18-168">To copy data from Amazon Marketplace Web Service, set the source type in the copy activity to **AmazonMWSSource**.</span></span> <span data-ttu-id="09a18-169">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="09a18-169">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="09a18-170">Property</span><span class="sxs-lookup"><span data-stu-id="09a18-170">Property</span></span> | <span data-ttu-id="09a18-171">Description</span><span class="sxs-lookup"><span data-stu-id="09a18-171">Description</span></span> | <span data-ttu-id="09a18-172">Required</span><span class="sxs-lookup"><span data-stu-id="09a18-172">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="09a18-173">type</span><span class="sxs-lookup"><span data-stu-id="09a18-173">type</span></span> | <span data-ttu-id="09a18-174">The type property of the copy activity source must be set to: **AmazonMWSSource**</span><span class="sxs-lookup"><span data-stu-id="09a18-174">The type property of the copy activity source must be set to: **AmazonMWSSource**</span></span> | <span data-ttu-id="09a18-175">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-175">Yes</span></span> |
| <span data-ttu-id="09a18-176">query</span><span class="sxs-lookup"><span data-stu-id="09a18-176">query</span></span> | <span data-ttu-id="09a18-177">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="09a18-177">Use the custom SQL query to read data.</span></span> <span data-ttu-id="09a18-178">For example: `"SELECT * FROM Orders where  Amazon_Order_Id = 'xx'"`.</span><span class="sxs-lookup"><span data-stu-id="09a18-178">For example: `"SELECT * FROM Orders where  Amazon_Order_Id = 'xx'"`.</span></span> | <span data-ttu-id="09a18-179">Yes</span><span class="sxs-lookup"><span data-stu-id="09a18-179">Yes</span></span> |

<span data-ttu-id="09a18-180">**Example:**</span><span class="sxs-lookup"><span data-stu-id="09a18-180">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromAmazonMWS",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<AmazonMWS input dataset name>",
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
                "type": "AmazonMWSSource",
                "query": "SELECT * FROM Orders where Amazon_Order_Id = 'xx'"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="09a18-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="09a18-181">Next steps</span></span>
<span data-ttu-id="09a18-182">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="09a18-182">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
