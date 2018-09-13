---
title: Copy data from Concur using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Concur to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 9414107e92bfb48bbf28348aa45c8ec6795dbd3f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870557"
---
# <a name="copy-data-from-concur-using-azure-data-factory"></a><span data-ttu-id="bda0f-103">Copy data from Concur using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bda0f-103">Copy data from Concur using Azure Data Factory</span></span>

<span data-ttu-id="bda0f-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Concur.</span><span class="sxs-lookup"><span data-stu-id="bda0f-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Concur.</span></span> <span data-ttu-id="bda0f-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="bda0f-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bda0f-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="bda0f-106">This connector is currently in preview.</span></span> <span data-ttu-id="bda0f-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="bda0f-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="bda0f-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="bda0f-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="bda0f-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="bda0f-109">Supported capabilities</span></span>

<span data-ttu-id="bda0f-110">You can copy data from Concur to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="bda0f-110">You can copy data from Concur to any supported sink data store.</span></span> <span data-ttu-id="bda0f-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="bda0f-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="bda0f-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="bda0f-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

> [!NOTE]
> <span data-ttu-id="bda0f-113">Partner account is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="bda0f-113">Partner account is currently not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bda0f-114">Getting started</span><span class="sxs-lookup"><span data-stu-id="bda0f-114">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="bda0f-115">The following sections provide details about properties that are used to define Data Factory entities specific to Concur connector.</span><span class="sxs-lookup"><span data-stu-id="bda0f-115">The following sections provide details about properties that are used to define Data Factory entities specific to Concur connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bda0f-116">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="bda0f-116">Linked service properties</span></span>

<span data-ttu-id="bda0f-117">The following properties are supported for Concur linked service:</span><span class="sxs-lookup"><span data-stu-id="bda0f-117">The following properties are supported for Concur linked service:</span></span>

| <span data-ttu-id="bda0f-118">Property</span><span class="sxs-lookup"><span data-stu-id="bda0f-118">Property</span></span> | <span data-ttu-id="bda0f-119">Description</span><span class="sxs-lookup"><span data-stu-id="bda0f-119">Description</span></span> | <span data-ttu-id="bda0f-120">Required</span><span class="sxs-lookup"><span data-stu-id="bda0f-120">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="bda0f-121">type</span><span class="sxs-lookup"><span data-stu-id="bda0f-121">type</span></span> | <span data-ttu-id="bda0f-122">The type property must be set to: **Concur**</span><span class="sxs-lookup"><span data-stu-id="bda0f-122">The type property must be set to: **Concur**</span></span> | <span data-ttu-id="bda0f-123">Yes</span><span class="sxs-lookup"><span data-stu-id="bda0f-123">Yes</span></span> |
| <span data-ttu-id="bda0f-124">clientId</span><span class="sxs-lookup"><span data-stu-id="bda0f-124">clientId</span></span> | <span data-ttu-id="bda0f-125">Application client_id supplied by Concur App Management.</span><span class="sxs-lookup"><span data-stu-id="bda0f-125">Application client_id supplied by Concur App Management.</span></span>  | <span data-ttu-id="bda0f-126">Yes</span><span class="sxs-lookup"><span data-stu-id="bda0f-126">Yes</span></span> |
| <span data-ttu-id="bda0f-127">username</span><span class="sxs-lookup"><span data-stu-id="bda0f-127">username</span></span> | <span data-ttu-id="bda0f-128">The user name that you use to access Concur Service.</span><span class="sxs-lookup"><span data-stu-id="bda0f-128">The user name that you use to access Concur Service.</span></span>  | <span data-ttu-id="bda0f-129">Yes</span><span class="sxs-lookup"><span data-stu-id="bda0f-129">Yes</span></span> |
| <span data-ttu-id="bda0f-130">password</span><span class="sxs-lookup"><span data-stu-id="bda0f-130">password</span></span> | <span data-ttu-id="bda0f-131">The password corresponding to the user name that you provided in the username field.</span><span class="sxs-lookup"><span data-stu-id="bda0f-131">The password corresponding to the user name that you provided in the username field.</span></span> <span data-ttu-id="bda0f-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="bda0f-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="bda0f-133">Yes</span><span class="sxs-lookup"><span data-stu-id="bda0f-133">Yes</span></span> |
| <span data-ttu-id="bda0f-134">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="bda0f-134">useEncryptedEndpoints</span></span> | <span data-ttu-id="bda0f-135">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bda0f-135">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="bda0f-136">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="bda0f-136">The default value is true.</span></span>  | <span data-ttu-id="bda0f-137">No</span><span class="sxs-lookup"><span data-stu-id="bda0f-137">No</span></span> |
| <span data-ttu-id="bda0f-138">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="bda0f-138">useHostVerification</span></span> | <span data-ttu-id="bda0f-139">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="bda0f-139">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="bda0f-140">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="bda0f-140">The default value is true.</span></span>  | <span data-ttu-id="bda0f-141">No</span><span class="sxs-lookup"><span data-stu-id="bda0f-141">No</span></span> |
| <span data-ttu-id="bda0f-142">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="bda0f-142">usePeerVerification</span></span> | <span data-ttu-id="bda0f-143">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="bda0f-143">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="bda0f-144">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="bda0f-144">The default value is true.</span></span>  | <span data-ttu-id="bda0f-145">No</span><span class="sxs-lookup"><span data-stu-id="bda0f-145">No</span></span> |

<span data-ttu-id="bda0f-146">**Example:**</span><span class="sxs-lookup"><span data-stu-id="bda0f-146">**Example:**</span></span>

```json
{
    "name": "ConcurLinkedService",
    "properties": {
        "type": "Concur",
        "typeProperties": {
            "clientId" : "<clientId>",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="bda0f-147">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="bda0f-147">Dataset properties</span></span>

<span data-ttu-id="bda0f-148">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="bda0f-148">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="bda0f-149">This section provides a list of properties supported by Concur dataset.</span><span class="sxs-lookup"><span data-stu-id="bda0f-149">This section provides a list of properties supported by Concur dataset.</span></span>

<span data-ttu-id="bda0f-150">To copy data from Concur, set the type property of the dataset to **ConcurObject**.</span><span class="sxs-lookup"><span data-stu-id="bda0f-150">To copy data from Concur, set the type property of the dataset to **ConcurObject**.</span></span> <span data-ttu-id="bda0f-151">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="bda0f-151">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="bda0f-152">**Example**</span><span class="sxs-lookup"><span data-stu-id="bda0f-152">**Example**</span></span>

```json
{
    "name": "ConcurDataset",
    "properties": {
        "type": "ConcurObject",
        "linkedServiceName": {
            "referenceName": "<Concur linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="bda0f-153">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="bda0f-153">Copy activity properties</span></span>

<span data-ttu-id="bda0f-154">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="bda0f-154">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="bda0f-155">This section provides a list of properties supported by Concur source.</span><span class="sxs-lookup"><span data-stu-id="bda0f-155">This section provides a list of properties supported by Concur source.</span></span>

### <a name="concursource-as-source"></a><span data-ttu-id="bda0f-156">ConcurSource as source</span><span class="sxs-lookup"><span data-stu-id="bda0f-156">ConcurSource as source</span></span>

<span data-ttu-id="bda0f-157">To copy data from Concur, set the source type in the copy activity to **ConcurSource**.</span><span class="sxs-lookup"><span data-stu-id="bda0f-157">To copy data from Concur, set the source type in the copy activity to **ConcurSource**.</span></span> <span data-ttu-id="bda0f-158">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="bda0f-158">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="bda0f-159">Property</span><span class="sxs-lookup"><span data-stu-id="bda0f-159">Property</span></span> | <span data-ttu-id="bda0f-160">Description</span><span class="sxs-lookup"><span data-stu-id="bda0f-160">Description</span></span> | <span data-ttu-id="bda0f-161">Required</span><span class="sxs-lookup"><span data-stu-id="bda0f-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="bda0f-162">type</span><span class="sxs-lookup"><span data-stu-id="bda0f-162">type</span></span> | <span data-ttu-id="bda0f-163">The type property of the copy activity source must be set to: **ConcurSource**</span><span class="sxs-lookup"><span data-stu-id="bda0f-163">The type property of the copy activity source must be set to: **ConcurSource**</span></span> | <span data-ttu-id="bda0f-164">Yes</span><span class="sxs-lookup"><span data-stu-id="bda0f-164">Yes</span></span> |
| <span data-ttu-id="bda0f-165">query</span><span class="sxs-lookup"><span data-stu-id="bda0f-165">query</span></span> | <span data-ttu-id="bda0f-166">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="bda0f-166">Use the custom SQL query to read data.</span></span> <span data-ttu-id="bda0f-167">For example: `"SELECT * FROM Opportunities where Id = xxx "`.</span><span class="sxs-lookup"><span data-stu-id="bda0f-167">For example: `"SELECT * FROM Opportunities where Id = xxx "`.</span></span> | <span data-ttu-id="bda0f-168">Yes</span><span class="sxs-lookup"><span data-stu-id="bda0f-168">Yes</span></span> |

<span data-ttu-id="bda0f-169">**Example:**</span><span class="sxs-lookup"><span data-stu-id="bda0f-169">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromConcur",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Concur input dataset name>",
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
                "type": "ConcurSource",
                "query": "SELECT * FROM Opportunities where Id = xxx"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="bda0f-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="bda0f-170">Next steps</span></span>
<span data-ttu-id="bda0f-171">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="bda0f-171">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
