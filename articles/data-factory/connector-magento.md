---
title: Copy data from Magento using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Magento to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: cdea8b6f24673186e3a3d2b44183b2c622aaaf41
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967553"
---
# <a name="copy-data-from-magento-using-azure-data-factory"></a><span data-ttu-id="86ad8-103">Copy data from Magento using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="86ad8-103">Copy data from Magento using Azure Data Factory</span></span>

<span data-ttu-id="86ad8-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Magento.</span><span class="sxs-lookup"><span data-stu-id="86ad8-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Magento.</span></span> <span data-ttu-id="86ad8-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="86ad8-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86ad8-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="86ad8-106">This connector is currently in preview.</span></span> <span data-ttu-id="86ad8-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="86ad8-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="86ad8-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="86ad8-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="86ad8-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="86ad8-109">Supported capabilities</span></span>

<span data-ttu-id="86ad8-110">You can copy data from Magento to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="86ad8-110">You can copy data from Magento to any supported sink data store.</span></span> <span data-ttu-id="86ad8-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="86ad8-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="86ad8-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="86ad8-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="86ad8-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="86ad8-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="86ad8-114">The following sections provide details about properties that are used to define Data Factory entities specific to Magento connector.</span><span class="sxs-lookup"><span data-stu-id="86ad8-114">The following sections provide details about properties that are used to define Data Factory entities specific to Magento connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="86ad8-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="86ad8-115">Linked service properties</span></span>

<span data-ttu-id="86ad8-116">The following properties are supported for Magento linked service:</span><span class="sxs-lookup"><span data-stu-id="86ad8-116">The following properties are supported for Magento linked service:</span></span>

| <span data-ttu-id="86ad8-117">Property</span><span class="sxs-lookup"><span data-stu-id="86ad8-117">Property</span></span> | <span data-ttu-id="86ad8-118">Description</span><span class="sxs-lookup"><span data-stu-id="86ad8-118">Description</span></span> | <span data-ttu-id="86ad8-119">Required</span><span class="sxs-lookup"><span data-stu-id="86ad8-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="86ad8-120">type</span><span class="sxs-lookup"><span data-stu-id="86ad8-120">type</span></span> | <span data-ttu-id="86ad8-121">The type property must be set to: **Magento**</span><span class="sxs-lookup"><span data-stu-id="86ad8-121">The type property must be set to: **Magento**</span></span> | <span data-ttu-id="86ad8-122">Yes</span><span class="sxs-lookup"><span data-stu-id="86ad8-122">Yes</span></span> |
| <span data-ttu-id="86ad8-123">host</span><span class="sxs-lookup"><span data-stu-id="86ad8-123">host</span></span> | <span data-ttu-id="86ad8-124">The URL of the Magento instance.</span><span class="sxs-lookup"><span data-stu-id="86ad8-124">The URL of the Magento instance.</span></span> <span data-ttu-id="86ad8-125">(that is, 192.168.222.110/magento3)</span><span class="sxs-lookup"><span data-stu-id="86ad8-125">(that is, 192.168.222.110/magento3)</span></span>  | <span data-ttu-id="86ad8-126">Yes</span><span class="sxs-lookup"><span data-stu-id="86ad8-126">Yes</span></span> |
| <span data-ttu-id="86ad8-127">accessToken</span><span class="sxs-lookup"><span data-stu-id="86ad8-127">accessToken</span></span> | <span data-ttu-id="86ad8-128">The access token from Magento.</span><span class="sxs-lookup"><span data-stu-id="86ad8-128">The access token from Magento.</span></span> <span data-ttu-id="86ad8-129">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="86ad8-129">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="86ad8-130">Yes</span><span class="sxs-lookup"><span data-stu-id="86ad8-130">Yes</span></span> |
| <span data-ttu-id="86ad8-131">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="86ad8-131">useEncryptedEndpoints</span></span> | <span data-ttu-id="86ad8-132">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="86ad8-132">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="86ad8-133">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="86ad8-133">The default value is true.</span></span>  | <span data-ttu-id="86ad8-134">No</span><span class="sxs-lookup"><span data-stu-id="86ad8-134">No</span></span> |
| <span data-ttu-id="86ad8-135">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="86ad8-135">useHostVerification</span></span> | <span data-ttu-id="86ad8-136">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="86ad8-136">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="86ad8-137">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="86ad8-137">The default value is true.</span></span>  | <span data-ttu-id="86ad8-138">No</span><span class="sxs-lookup"><span data-stu-id="86ad8-138">No</span></span> |
| <span data-ttu-id="86ad8-139">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="86ad8-139">usePeerVerification</span></span> | <span data-ttu-id="86ad8-140">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="86ad8-140">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="86ad8-141">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="86ad8-141">The default value is true.</span></span>  | <span data-ttu-id="86ad8-142">No</span><span class="sxs-lookup"><span data-stu-id="86ad8-142">No</span></span> |

<span data-ttu-id="86ad8-143">**Example:**</span><span class="sxs-lookup"><span data-stu-id="86ad8-143">**Example:**</span></span>

```json
{
    "name": "MagentoLinkedService",
    "properties": {
        "type": "Magento",
        "typeProperties": {
            "host" : "192.168.222.110/magento3",
            "accessToken": {
                 "type": "SecureString",
                 "value": "<accessToken>"
            },
            "useEncryptedEndpoints" : true,
            "useHostVerification" : true,
            "usePeerVerification" : true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="86ad8-144">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="86ad8-144">Dataset properties</span></span>

<span data-ttu-id="86ad8-145">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="86ad8-145">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="86ad8-146">This section provides a list of properties supported by Magento dataset.</span><span class="sxs-lookup"><span data-stu-id="86ad8-146">This section provides a list of properties supported by Magento dataset.</span></span>

<span data-ttu-id="86ad8-147">To copy data from Magento, set the type property of the dataset to **MagentoObject**.</span><span class="sxs-lookup"><span data-stu-id="86ad8-147">To copy data from Magento, set the type property of the dataset to **MagentoObject**.</span></span> <span data-ttu-id="86ad8-148">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="86ad8-148">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="86ad8-149">**Example**</span><span class="sxs-lookup"><span data-stu-id="86ad8-149">**Example**</span></span>

```json
{
    "name": "MagentoDataset",
    "properties": {
        "type": "MagentoObject",
        "linkedServiceName": {
            "referenceName": "<Magento linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="86ad8-150">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="86ad8-150">Copy activity properties</span></span>

<span data-ttu-id="86ad8-151">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="86ad8-151">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="86ad8-152">This section provides a list of properties supported by Magento source.</span><span class="sxs-lookup"><span data-stu-id="86ad8-152">This section provides a list of properties supported by Magento source.</span></span>

### <a name="magentosource-as-source"></a><span data-ttu-id="86ad8-153">MagentoSource as source</span><span class="sxs-lookup"><span data-stu-id="86ad8-153">MagentoSource as source</span></span>

<span data-ttu-id="86ad8-154">To copy data from Magento, set the source type in the copy activity to **MagentoSource**.</span><span class="sxs-lookup"><span data-stu-id="86ad8-154">To copy data from Magento, set the source type in the copy activity to **MagentoSource**.</span></span> <span data-ttu-id="86ad8-155">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="86ad8-155">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="86ad8-156">Property</span><span class="sxs-lookup"><span data-stu-id="86ad8-156">Property</span></span> | <span data-ttu-id="86ad8-157">Description</span><span class="sxs-lookup"><span data-stu-id="86ad8-157">Description</span></span> | <span data-ttu-id="86ad8-158">Required</span><span class="sxs-lookup"><span data-stu-id="86ad8-158">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="86ad8-159">type</span><span class="sxs-lookup"><span data-stu-id="86ad8-159">type</span></span> | <span data-ttu-id="86ad8-160">The type property of the copy activity source must be set to: **MagentoSource**</span><span class="sxs-lookup"><span data-stu-id="86ad8-160">The type property of the copy activity source must be set to: **MagentoSource**</span></span> | <span data-ttu-id="86ad8-161">Yes</span><span class="sxs-lookup"><span data-stu-id="86ad8-161">Yes</span></span> |
| <span data-ttu-id="86ad8-162">query</span><span class="sxs-lookup"><span data-stu-id="86ad8-162">query</span></span> | <span data-ttu-id="86ad8-163">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="86ad8-163">Use the custom SQL query to read data.</span></span> <span data-ttu-id="86ad8-164">For example: `"SELECT * FROM Customers"`.</span><span class="sxs-lookup"><span data-stu-id="86ad8-164">For example: `"SELECT * FROM Customers"`.</span></span> | <span data-ttu-id="86ad8-165">Yes</span><span class="sxs-lookup"><span data-stu-id="86ad8-165">Yes</span></span> |

<span data-ttu-id="86ad8-166">**Example:**</span><span class="sxs-lookup"><span data-stu-id="86ad8-166">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromMagento",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Magento input dataset name>",
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
                "type": "MagentoSource",
                "query": "SELECT * FROM Customers where Id > XXX"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="86ad8-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="86ad8-167">Next steps</span></span>
<span data-ttu-id="86ad8-168">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="86ad8-168">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
