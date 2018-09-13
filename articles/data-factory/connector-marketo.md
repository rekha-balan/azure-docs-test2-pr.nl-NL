---
title: Copy data from Marketo using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Marketo to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: f9571f610310a78b8c56732a71ea96f638d59d50
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856371"
---
# <a name="copy-data-from-marketo-using-azure-data-factory"></a><span data-ttu-id="c03aa-103">Copy data from Marketo using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c03aa-103">Copy data from Marketo using Azure Data Factory</span></span>

<span data-ttu-id="c03aa-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Marketo.</span><span class="sxs-lookup"><span data-stu-id="c03aa-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Marketo.</span></span> <span data-ttu-id="c03aa-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="c03aa-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c03aa-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="c03aa-106">This connector is currently in preview.</span></span> <span data-ttu-id="c03aa-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="c03aa-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="c03aa-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="c03aa-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="c03aa-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="c03aa-109">Supported capabilities</span></span>

<span data-ttu-id="c03aa-110">You can copy data from Marketo to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="c03aa-110">You can copy data from Marketo to any supported sink data store.</span></span> <span data-ttu-id="c03aa-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="c03aa-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="c03aa-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="c03aa-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c03aa-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="c03aa-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="c03aa-114">The following sections provide details about properties that are used to define Data Factory entities specific to Marketo connector.</span><span class="sxs-lookup"><span data-stu-id="c03aa-114">The following sections provide details about properties that are used to define Data Factory entities specific to Marketo connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c03aa-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="c03aa-115">Linked service properties</span></span>

<span data-ttu-id="c03aa-116">The following properties are supported for Marketo linked service:</span><span class="sxs-lookup"><span data-stu-id="c03aa-116">The following properties are supported for Marketo linked service:</span></span>

| <span data-ttu-id="c03aa-117">Property</span><span class="sxs-lookup"><span data-stu-id="c03aa-117">Property</span></span> | <span data-ttu-id="c03aa-118">Description</span><span class="sxs-lookup"><span data-stu-id="c03aa-118">Description</span></span> | <span data-ttu-id="c03aa-119">Required</span><span class="sxs-lookup"><span data-stu-id="c03aa-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c03aa-120">type</span><span class="sxs-lookup"><span data-stu-id="c03aa-120">type</span></span> | <span data-ttu-id="c03aa-121">The type property must be set to: **Marketo**</span><span class="sxs-lookup"><span data-stu-id="c03aa-121">The type property must be set to: **Marketo**</span></span> | <span data-ttu-id="c03aa-122">Yes</span><span class="sxs-lookup"><span data-stu-id="c03aa-122">Yes</span></span> |
| <span data-ttu-id="c03aa-123">endpoint</span><span class="sxs-lookup"><span data-stu-id="c03aa-123">endpoint</span></span> | <span data-ttu-id="c03aa-124">The endpoint of the Marketo server.</span><span class="sxs-lookup"><span data-stu-id="c03aa-124">The endpoint of the Marketo server.</span></span> <span data-ttu-id="c03aa-125">(i.e. 123-ABC-321.mktorest.com)</span><span class="sxs-lookup"><span data-stu-id="c03aa-125">(i.e. 123-ABC-321.mktorest.com)</span></span>  | <span data-ttu-id="c03aa-126">Yes</span><span class="sxs-lookup"><span data-stu-id="c03aa-126">Yes</span></span> |
| <span data-ttu-id="c03aa-127">clientId</span><span class="sxs-lookup"><span data-stu-id="c03aa-127">clientId</span></span> | <span data-ttu-id="c03aa-128">The client Id of your Marketo service.</span><span class="sxs-lookup"><span data-stu-id="c03aa-128">The client Id of your Marketo service.</span></span>  | <span data-ttu-id="c03aa-129">Yes</span><span class="sxs-lookup"><span data-stu-id="c03aa-129">Yes</span></span> |
| <span data-ttu-id="c03aa-130">clientSecret</span><span class="sxs-lookup"><span data-stu-id="c03aa-130">clientSecret</span></span> | <span data-ttu-id="c03aa-131">The client secret of your Marketo service.</span><span class="sxs-lookup"><span data-stu-id="c03aa-131">The client secret of your Marketo service.</span></span> <span data-ttu-id="c03aa-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="c03aa-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="c03aa-133">Yes</span><span class="sxs-lookup"><span data-stu-id="c03aa-133">Yes</span></span> |
| <span data-ttu-id="c03aa-134">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="c03aa-134">useEncryptedEndpoints</span></span> | <span data-ttu-id="c03aa-135">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c03aa-135">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="c03aa-136">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="c03aa-136">The default value is true.</span></span>  | <span data-ttu-id="c03aa-137">No</span><span class="sxs-lookup"><span data-stu-id="c03aa-137">No</span></span> |
| <span data-ttu-id="c03aa-138">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="c03aa-138">useHostVerification</span></span> | <span data-ttu-id="c03aa-139">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="c03aa-139">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="c03aa-140">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="c03aa-140">The default value is true.</span></span>  | <span data-ttu-id="c03aa-141">No</span><span class="sxs-lookup"><span data-stu-id="c03aa-141">No</span></span> |
| <span data-ttu-id="c03aa-142">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="c03aa-142">usePeerVerification</span></span> | <span data-ttu-id="c03aa-143">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="c03aa-143">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="c03aa-144">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="c03aa-144">The default value is true.</span></span>  | <span data-ttu-id="c03aa-145">No</span><span class="sxs-lookup"><span data-stu-id="c03aa-145">No</span></span> |

<span data-ttu-id="c03aa-146">**Example:**</span><span class="sxs-lookup"><span data-stu-id="c03aa-146">**Example:**</span></span>

```json
{
    "name": "MarketoLinkedService",
    "properties": {
        "type": "Marketo",
        "typeProperties": {
            "endpoint" : "123-ABC-321.mktorest.com",
            "clientId" : "<clientId>",
            "clientSecret": {
                 "type": "SecureString",
                 "value": "<clientSecret>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c03aa-147">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="c03aa-147">Dataset properties</span></span>

<span data-ttu-id="c03aa-148">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="c03aa-148">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="c03aa-149">This section provides a list of properties supported by Marketo dataset.</span><span class="sxs-lookup"><span data-stu-id="c03aa-149">This section provides a list of properties supported by Marketo dataset.</span></span>

<span data-ttu-id="c03aa-150">To copy data from Marketo, set the type property of the dataset to **MarketoObject**.</span><span class="sxs-lookup"><span data-stu-id="c03aa-150">To copy data from Marketo, set the type property of the dataset to **MarketoObject**.</span></span> <span data-ttu-id="c03aa-151">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="c03aa-151">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="c03aa-152">**Example**</span><span class="sxs-lookup"><span data-stu-id="c03aa-152">**Example**</span></span>

```json
{
    "name": "MarketoDataset",
    "properties": {
        "type": "MarketoObject",
        "linkedServiceName": {
            "referenceName": "<Marketo linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="c03aa-153">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="c03aa-153">Copy activity properties</span></span>

<span data-ttu-id="c03aa-154">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="c03aa-154">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="c03aa-155">This section provides a list of properties supported by Marketo source.</span><span class="sxs-lookup"><span data-stu-id="c03aa-155">This section provides a list of properties supported by Marketo source.</span></span>

### <a name="marketosource-as-source"></a><span data-ttu-id="c03aa-156">MarketoSource as source</span><span class="sxs-lookup"><span data-stu-id="c03aa-156">MarketoSource as source</span></span>

<span data-ttu-id="c03aa-157">To copy data from Marketo, set the source type in the copy activity to **MarketoSource**.</span><span class="sxs-lookup"><span data-stu-id="c03aa-157">To copy data from Marketo, set the source type in the copy activity to **MarketoSource**.</span></span> <span data-ttu-id="c03aa-158">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="c03aa-158">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="c03aa-159">Property</span><span class="sxs-lookup"><span data-stu-id="c03aa-159">Property</span></span> | <span data-ttu-id="c03aa-160">Description</span><span class="sxs-lookup"><span data-stu-id="c03aa-160">Description</span></span> | <span data-ttu-id="c03aa-161">Required</span><span class="sxs-lookup"><span data-stu-id="c03aa-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c03aa-162">type</span><span class="sxs-lookup"><span data-stu-id="c03aa-162">type</span></span> | <span data-ttu-id="c03aa-163">The type property of the copy activity source must be set to: **MarketoSource**</span><span class="sxs-lookup"><span data-stu-id="c03aa-163">The type property of the copy activity source must be set to: **MarketoSource**</span></span> | <span data-ttu-id="c03aa-164">Yes</span><span class="sxs-lookup"><span data-stu-id="c03aa-164">Yes</span></span> |
| <span data-ttu-id="c03aa-165">query</span><span class="sxs-lookup"><span data-stu-id="c03aa-165">query</span></span> | <span data-ttu-id="c03aa-166">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="c03aa-166">Use the custom SQL query to read data.</span></span> <span data-ttu-id="c03aa-167">For example: `"SELECT * FROM Activitiy_Types"`.</span><span class="sxs-lookup"><span data-stu-id="c03aa-167">For example: `"SELECT * FROM Activitiy_Types"`.</span></span> | <span data-ttu-id="c03aa-168">Yes</span><span class="sxs-lookup"><span data-stu-id="c03aa-168">Yes</span></span> |

<span data-ttu-id="c03aa-169">**Example:**</span><span class="sxs-lookup"><span data-stu-id="c03aa-169">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromMarketo",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Marketo input dataset name>",
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
                "type": "MarketoSource",
                "query": "SELECT top 1000 * FROM Activitiy_Types"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="c03aa-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="c03aa-170">Next steps</span></span>
<span data-ttu-id="c03aa-171">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c03aa-171">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
