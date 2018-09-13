---
title: Copy data from Zoho using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Zoho to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: aa87e111bad1af03e2778bcbfc452c291bc72a81
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857346"
---
# <a name="copy-data-from-zoho-using-azure-data-factory"></a><span data-ttu-id="b2255-103">Copy data from Zoho using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b2255-103">Copy data from Zoho using Azure Data Factory</span></span>

<span data-ttu-id="b2255-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Zoho.</span><span class="sxs-lookup"><span data-stu-id="b2255-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Zoho.</span></span> <span data-ttu-id="b2255-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="b2255-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b2255-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="b2255-106">This connector is currently in preview.</span></span> <span data-ttu-id="b2255-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="b2255-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="b2255-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="b2255-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="b2255-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="b2255-109">Supported capabilities</span></span>

<span data-ttu-id="b2255-110">You can copy data from Zoho to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="b2255-110">You can copy data from Zoho to any supported sink data store.</span></span> <span data-ttu-id="b2255-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="b2255-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="b2255-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="b2255-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b2255-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="b2255-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="b2255-114">The following sections provide details about properties that are used to define Data Factory entities specific to Zoho connector.</span><span class="sxs-lookup"><span data-stu-id="b2255-114">The following sections provide details about properties that are used to define Data Factory entities specific to Zoho connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b2255-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="b2255-115">Linked service properties</span></span>

<span data-ttu-id="b2255-116">The following properties are supported for Zoho linked service:</span><span class="sxs-lookup"><span data-stu-id="b2255-116">The following properties are supported for Zoho linked service:</span></span>

| <span data-ttu-id="b2255-117">Property</span><span class="sxs-lookup"><span data-stu-id="b2255-117">Property</span></span> | <span data-ttu-id="b2255-118">Description</span><span class="sxs-lookup"><span data-stu-id="b2255-118">Description</span></span> | <span data-ttu-id="b2255-119">Required</span><span class="sxs-lookup"><span data-stu-id="b2255-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b2255-120">type</span><span class="sxs-lookup"><span data-stu-id="b2255-120">type</span></span> | <span data-ttu-id="b2255-121">The type property must be set to: **Zoho**</span><span class="sxs-lookup"><span data-stu-id="b2255-121">The type property must be set to: **Zoho**</span></span> | <span data-ttu-id="b2255-122">Yes</span><span class="sxs-lookup"><span data-stu-id="b2255-122">Yes</span></span> |
| <span data-ttu-id="b2255-123">endpoint</span><span class="sxs-lookup"><span data-stu-id="b2255-123">endpoint</span></span> | <span data-ttu-id="b2255-124">The endpoint of the Zoho server (`crm.zoho.com/crm/private`).</span><span class="sxs-lookup"><span data-stu-id="b2255-124">The endpoint of the Zoho server (`crm.zoho.com/crm/private`).</span></span> | <span data-ttu-id="b2255-125">Yes</span><span class="sxs-lookup"><span data-stu-id="b2255-125">Yes</span></span> |
| <span data-ttu-id="b2255-126">accessToken</span><span class="sxs-lookup"><span data-stu-id="b2255-126">accessToken</span></span> | <span data-ttu-id="b2255-127">The access token for Zoho authentication.</span><span class="sxs-lookup"><span data-stu-id="b2255-127">The access token for Zoho authentication.</span></span> <span data-ttu-id="b2255-128">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="b2255-128">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="b2255-129">Yes</span><span class="sxs-lookup"><span data-stu-id="b2255-129">Yes</span></span> |
| <span data-ttu-id="b2255-130">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="b2255-130">useEncryptedEndpoints</span></span> | <span data-ttu-id="b2255-131">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b2255-131">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="b2255-132">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="b2255-132">The default value is true.</span></span>  | <span data-ttu-id="b2255-133">No</span><span class="sxs-lookup"><span data-stu-id="b2255-133">No</span></span> |
| <span data-ttu-id="b2255-134">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="b2255-134">useHostVerification</span></span> | <span data-ttu-id="b2255-135">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="b2255-135">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="b2255-136">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="b2255-136">The default value is true.</span></span>  | <span data-ttu-id="b2255-137">No</span><span class="sxs-lookup"><span data-stu-id="b2255-137">No</span></span> |
| <span data-ttu-id="b2255-138">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="b2255-138">usePeerVerification</span></span> | <span data-ttu-id="b2255-139">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="b2255-139">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="b2255-140">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="b2255-140">The default value is true.</span></span>  | <span data-ttu-id="b2255-141">No</span><span class="sxs-lookup"><span data-stu-id="b2255-141">No</span></span> |

<span data-ttu-id="b2255-142">**Example:**</span><span class="sxs-lookup"><span data-stu-id="b2255-142">**Example:**</span></span>

```json
{
    "name": "ZohoLinkedService",
    "properties": {
        "type": "Zoho",
        "typeProperties": {
            "endpoint" : "crm.zoho.com/crm/private",
            "accessToken": {
                 "type": "SecureString",
                 "value": "<accessToken>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="b2255-143">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="b2255-143">Dataset properties</span></span>

<span data-ttu-id="b2255-144">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="b2255-144">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="b2255-145">This section provides a list of properties supported by Zoho dataset.</span><span class="sxs-lookup"><span data-stu-id="b2255-145">This section provides a list of properties supported by Zoho dataset.</span></span>

<span data-ttu-id="b2255-146">To copy data from Zoho, set the type property of the dataset to **ZohoObject**.</span><span class="sxs-lookup"><span data-stu-id="b2255-146">To copy data from Zoho, set the type property of the dataset to **ZohoObject**.</span></span> <span data-ttu-id="b2255-147">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="b2255-147">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="b2255-148">**Example**</span><span class="sxs-lookup"><span data-stu-id="b2255-148">**Example**</span></span>

```json
{
    "name": "ZohoDataset",
    "properties": {
        "type": "ZohoObject",
        "linkedServiceName": {
            "referenceName": "<Zoho linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="b2255-149">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="b2255-149">Copy activity properties</span></span>

<span data-ttu-id="b2255-150">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="b2255-150">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="b2255-151">This section provides a list of properties supported by Zoho source.</span><span class="sxs-lookup"><span data-stu-id="b2255-151">This section provides a list of properties supported by Zoho source.</span></span>

### <a name="zohosource-as-source"></a><span data-ttu-id="b2255-152">ZohoSource as source</span><span class="sxs-lookup"><span data-stu-id="b2255-152">ZohoSource as source</span></span>

<span data-ttu-id="b2255-153">To copy data from Zoho, set the source type in the copy activity to **ZohoSource**.</span><span class="sxs-lookup"><span data-stu-id="b2255-153">To copy data from Zoho, set the source type in the copy activity to **ZohoSource**.</span></span> <span data-ttu-id="b2255-154">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="b2255-154">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="b2255-155">Property</span><span class="sxs-lookup"><span data-stu-id="b2255-155">Property</span></span> | <span data-ttu-id="b2255-156">Description</span><span class="sxs-lookup"><span data-stu-id="b2255-156">Description</span></span> | <span data-ttu-id="b2255-157">Required</span><span class="sxs-lookup"><span data-stu-id="b2255-157">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b2255-158">type</span><span class="sxs-lookup"><span data-stu-id="b2255-158">type</span></span> | <span data-ttu-id="b2255-159">The type property of the copy activity source must be set to: **ZohoSource**</span><span class="sxs-lookup"><span data-stu-id="b2255-159">The type property of the copy activity source must be set to: **ZohoSource**</span></span> | <span data-ttu-id="b2255-160">Yes</span><span class="sxs-lookup"><span data-stu-id="b2255-160">Yes</span></span> |
| <span data-ttu-id="b2255-161">query</span><span class="sxs-lookup"><span data-stu-id="b2255-161">query</span></span> | <span data-ttu-id="b2255-162">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="b2255-162">Use the custom SQL query to read data.</span></span> <span data-ttu-id="b2255-163">For example: `"SELECT * FROM Accounts"`.</span><span class="sxs-lookup"><span data-stu-id="b2255-163">For example: `"SELECT * FROM Accounts"`.</span></span> | <span data-ttu-id="b2255-164">Yes</span><span class="sxs-lookup"><span data-stu-id="b2255-164">Yes</span></span> |

<span data-ttu-id="b2255-165">**Example:**</span><span class="sxs-lookup"><span data-stu-id="b2255-165">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromZoho",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Zoho input dataset name>",
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
                "type": "ZohoSource",
                "query": "SELECT * FROM Accounts"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="b2255-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2255-166">Next steps</span></span>
<span data-ttu-id="b2255-167">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b2255-167">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
