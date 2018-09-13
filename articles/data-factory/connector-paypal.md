---
title: Copy data from PayPal using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from PayPal to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 844b9979ed3bb61850ff9448d065bc1300fe23d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965897"
---
# <a name="copy-data-from-paypal-using-azure-data-factory"></a><span data-ttu-id="2c726-103">Copy data from PayPal using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2c726-103">Copy data from PayPal using Azure Data Factory</span></span>

<span data-ttu-id="2c726-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from PayPal.</span><span class="sxs-lookup"><span data-stu-id="2c726-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from PayPal.</span></span> <span data-ttu-id="2c726-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="2c726-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c726-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="2c726-106">This connector is currently in preview.</span></span> <span data-ttu-id="2c726-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="2c726-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="2c726-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="2c726-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="2c726-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="2c726-109">Supported capabilities</span></span>

<span data-ttu-id="2c726-110">You can copy data from PayPal to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="2c726-110">You can copy data from PayPal to any supported sink data store.</span></span> <span data-ttu-id="2c726-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="2c726-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="2c726-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="2c726-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2c726-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="2c726-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="2c726-114">The following sections provide details about properties that are used to define Data Factory entities specific to PayPal connector.</span><span class="sxs-lookup"><span data-stu-id="2c726-114">The following sections provide details about properties that are used to define Data Factory entities specific to PayPal connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2c726-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="2c726-115">Linked service properties</span></span>

<span data-ttu-id="2c726-116">The following properties are supported for PayPal linked service:</span><span class="sxs-lookup"><span data-stu-id="2c726-116">The following properties are supported for PayPal linked service:</span></span>

| <span data-ttu-id="2c726-117">Property</span><span class="sxs-lookup"><span data-stu-id="2c726-117">Property</span></span> | <span data-ttu-id="2c726-118">Description</span><span class="sxs-lookup"><span data-stu-id="2c726-118">Description</span></span> | <span data-ttu-id="2c726-119">Required</span><span class="sxs-lookup"><span data-stu-id="2c726-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2c726-120">type</span><span class="sxs-lookup"><span data-stu-id="2c726-120">type</span></span> | <span data-ttu-id="2c726-121">The type property must be set to: **PayPal**</span><span class="sxs-lookup"><span data-stu-id="2c726-121">The type property must be set to: **PayPal**</span></span> | <span data-ttu-id="2c726-122">Yes</span><span class="sxs-lookup"><span data-stu-id="2c726-122">Yes</span></span> |
| <span data-ttu-id="2c726-123">host</span><span class="sxs-lookup"><span data-stu-id="2c726-123">host</span></span> | <span data-ttu-id="2c726-124">The URL of the PayPal instance.</span><span class="sxs-lookup"><span data-stu-id="2c726-124">The URL of the PayPal instance.</span></span> <span data-ttu-id="2c726-125">(that is, api.sandbox.paypal.com)</span><span class="sxs-lookup"><span data-stu-id="2c726-125">(that is, api.sandbox.paypal.com)</span></span>  | <span data-ttu-id="2c726-126">Yes</span><span class="sxs-lookup"><span data-stu-id="2c726-126">Yes</span></span> |
| <span data-ttu-id="2c726-127">clientId</span><span class="sxs-lookup"><span data-stu-id="2c726-127">clientId</span></span> | <span data-ttu-id="2c726-128">The client ID associated with your PayPal application.</span><span class="sxs-lookup"><span data-stu-id="2c726-128">The client ID associated with your PayPal application.</span></span>  | <span data-ttu-id="2c726-129">Yes</span><span class="sxs-lookup"><span data-stu-id="2c726-129">Yes</span></span> |
| <span data-ttu-id="2c726-130">clientSecret</span><span class="sxs-lookup"><span data-stu-id="2c726-130">clientSecret</span></span> | <span data-ttu-id="2c726-131">The client secret associated with your PayPal application.</span><span class="sxs-lookup"><span data-stu-id="2c726-131">The client secret associated with your PayPal application.</span></span> <span data-ttu-id="2c726-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="2c726-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="2c726-133">Yes</span><span class="sxs-lookup"><span data-stu-id="2c726-133">Yes</span></span> |
| <span data-ttu-id="2c726-134">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="2c726-134">useEncryptedEndpoints</span></span> | <span data-ttu-id="2c726-135">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2c726-135">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="2c726-136">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="2c726-136">The default value is true.</span></span>  | <span data-ttu-id="2c726-137">No</span><span class="sxs-lookup"><span data-stu-id="2c726-137">No</span></span> |
| <span data-ttu-id="2c726-138">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="2c726-138">useHostVerification</span></span> | <span data-ttu-id="2c726-139">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="2c726-139">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="2c726-140">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="2c726-140">The default value is true.</span></span>  | <span data-ttu-id="2c726-141">No</span><span class="sxs-lookup"><span data-stu-id="2c726-141">No</span></span> |
| <span data-ttu-id="2c726-142">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="2c726-142">usePeerVerification</span></span> | <span data-ttu-id="2c726-143">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="2c726-143">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="2c726-144">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="2c726-144">The default value is true.</span></span>  | <span data-ttu-id="2c726-145">No</span><span class="sxs-lookup"><span data-stu-id="2c726-145">No</span></span> |

<span data-ttu-id="2c726-146">**Example:**</span><span class="sxs-lookup"><span data-stu-id="2c726-146">**Example:**</span></span>

```json
{
    "name": "PayPalLinkedService",
    "properties": {
        "type": "PayPal",
        "typeProperties": {
            "host" : "api.sandbox.paypal.com",
            "clientId" : "<clientId>",
            "clientSecret": {
                 "type": "SecureString",
                 "value": "<clientSecret>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="2c726-147">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="2c726-147">Dataset properties</span></span>

<span data-ttu-id="2c726-148">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="2c726-148">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="2c726-149">This section provides a list of properties supported by PayPal dataset.</span><span class="sxs-lookup"><span data-stu-id="2c726-149">This section provides a list of properties supported by PayPal dataset.</span></span>

<span data-ttu-id="2c726-150">To copy data from PayPal, set the type property of the dataset to **PayPalObject**.</span><span class="sxs-lookup"><span data-stu-id="2c726-150">To copy data from PayPal, set the type property of the dataset to **PayPalObject**.</span></span> <span data-ttu-id="2c726-151">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="2c726-151">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="2c726-152">**Example**</span><span class="sxs-lookup"><span data-stu-id="2c726-152">**Example**</span></span>

```json
{
    "name": "PayPalDataset",
    "properties": {
        "type": "PayPalObject",
        "linkedServiceName": {
            "referenceName": "<PayPal linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="2c726-153">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="2c726-153">Copy activity properties</span></span>

<span data-ttu-id="2c726-154">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="2c726-154">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="2c726-155">This section provides a list of properties supported by PayPal source.</span><span class="sxs-lookup"><span data-stu-id="2c726-155">This section provides a list of properties supported by PayPal source.</span></span>

### <a name="paypalsource-as-source"></a><span data-ttu-id="2c726-156">PayPalSource as source</span><span class="sxs-lookup"><span data-stu-id="2c726-156">PayPalSource as source</span></span>

<span data-ttu-id="2c726-157">To copy data from PayPal, set the source type in the copy activity to **PayPalSource**.</span><span class="sxs-lookup"><span data-stu-id="2c726-157">To copy data from PayPal, set the source type in the copy activity to **PayPalSource**.</span></span> <span data-ttu-id="2c726-158">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="2c726-158">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="2c726-159">Property</span><span class="sxs-lookup"><span data-stu-id="2c726-159">Property</span></span> | <span data-ttu-id="2c726-160">Description</span><span class="sxs-lookup"><span data-stu-id="2c726-160">Description</span></span> | <span data-ttu-id="2c726-161">Required</span><span class="sxs-lookup"><span data-stu-id="2c726-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2c726-162">type</span><span class="sxs-lookup"><span data-stu-id="2c726-162">type</span></span> | <span data-ttu-id="2c726-163">The type property of the copy activity source must be set to: **PayPalSource**</span><span class="sxs-lookup"><span data-stu-id="2c726-163">The type property of the copy activity source must be set to: **PayPalSource**</span></span> | <span data-ttu-id="2c726-164">Yes</span><span class="sxs-lookup"><span data-stu-id="2c726-164">Yes</span></span> |
| <span data-ttu-id="2c726-165">query</span><span class="sxs-lookup"><span data-stu-id="2c726-165">query</span></span> | <span data-ttu-id="2c726-166">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="2c726-166">Use the custom SQL query to read data.</span></span> <span data-ttu-id="2c726-167">For example: `"SELECT * FROM Payment_Experience"`.</span><span class="sxs-lookup"><span data-stu-id="2c726-167">For example: `"SELECT * FROM Payment_Experience"`.</span></span> | <span data-ttu-id="2c726-168">Yes</span><span class="sxs-lookup"><span data-stu-id="2c726-168">Yes</span></span> |

<span data-ttu-id="2c726-169">**Example:**</span><span class="sxs-lookup"><span data-stu-id="2c726-169">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromPayPal",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<PayPal input dataset name>",
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
                "type": "PayPalSource",
                "query": "SELECT * FROM Payment_Experience"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="2c726-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c726-170">Next steps</span></span>
<span data-ttu-id="2c726-171">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2c726-171">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
