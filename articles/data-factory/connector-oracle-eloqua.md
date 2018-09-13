---
title: Copy data from Oracle Eloqua using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Oracle Eloqua to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 06/22/2018
ms.author: jingwang
ms.openlocfilehash: 821e345933ba52ed2c71251bab3ba159e5412568
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856983"
---
# <a name="copy-data-from-oracle-eloqua-using-azure-data-factory"></a><span data-ttu-id="93b27-103">Copy data from Oracle Eloqua using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="93b27-103">Copy data from Oracle Eloqua using Azure Data Factory</span></span>

<span data-ttu-id="93b27-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Oracle Eloqua.</span><span class="sxs-lookup"><span data-stu-id="93b27-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Oracle Eloqua.</span></span> <span data-ttu-id="93b27-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="93b27-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93b27-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="93b27-106">This connector is currently in preview.</span></span> <span data-ttu-id="93b27-107">You can try it out and provide feedback.</span><span class="sxs-lookup"><span data-stu-id="93b27-107">You can try it out and provide feedback.</span></span> <span data-ttu-id="93b27-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="93b27-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="93b27-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="93b27-109">Supported capabilities</span></span>

<span data-ttu-id="93b27-110">You can copy data from Oracle Eloqua to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="93b27-110">You can copy data from Oracle Eloqua to any supported sink data store.</span></span> <span data-ttu-id="93b27-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="93b27-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="93b27-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="93b27-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="93b27-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="93b27-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="93b27-114">The following sections provide details about properties that are used to define Data Factory entities specific to Oracle Eloqua connector.</span><span class="sxs-lookup"><span data-stu-id="93b27-114">The following sections provide details about properties that are used to define Data Factory entities specific to Oracle Eloqua connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="93b27-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="93b27-115">Linked service properties</span></span>

<span data-ttu-id="93b27-116">The following properties are supported for Oracle Eloqua linked service:</span><span class="sxs-lookup"><span data-stu-id="93b27-116">The following properties are supported for Oracle Eloqua linked service:</span></span>

| <span data-ttu-id="93b27-117">Property</span><span class="sxs-lookup"><span data-stu-id="93b27-117">Property</span></span> | <span data-ttu-id="93b27-118">Description</span><span class="sxs-lookup"><span data-stu-id="93b27-118">Description</span></span> | <span data-ttu-id="93b27-119">Required</span><span class="sxs-lookup"><span data-stu-id="93b27-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="93b27-120">type</span><span class="sxs-lookup"><span data-stu-id="93b27-120">type</span></span> | <span data-ttu-id="93b27-121">The type property must be set to: **Eloqua**</span><span class="sxs-lookup"><span data-stu-id="93b27-121">The type property must be set to: **Eloqua**</span></span> | <span data-ttu-id="93b27-122">Yes</span><span class="sxs-lookup"><span data-stu-id="93b27-122">Yes</span></span> |
| <span data-ttu-id="93b27-123">endpoint</span><span class="sxs-lookup"><span data-stu-id="93b27-123">endpoint</span></span> | <span data-ttu-id="93b27-124">The endpoint of the Eloqua server.</span><span class="sxs-lookup"><span data-stu-id="93b27-124">The endpoint of the Eloqua server.</span></span> <span data-ttu-id="93b27-125">Eloqua supports multiple data centers, to determine your endpoint, login to https://login.eloqua.com with your credential, then copy the **base URL** portion from the redirected URL with the pattern of `xxx.xxx.eloqua.com`.</span><span class="sxs-lookup"><span data-stu-id="93b27-125">Eloqua supports multiple data centers, to determine your endpoint, login to https://login.eloqua.com with your credential, then copy the **base URL** portion from the redirected URL with the pattern of `xxx.xxx.eloqua.com`.</span></span> | <span data-ttu-id="93b27-126">Yes</span><span class="sxs-lookup"><span data-stu-id="93b27-126">Yes</span></span> |
| <span data-ttu-id="93b27-127">username</span><span class="sxs-lookup"><span data-stu-id="93b27-127">username</span></span> | <span data-ttu-id="93b27-128">The site name and user name of your Eloqua account in the form: `SiteName\Username` e.g. `Eloqua\Alice`.</span><span class="sxs-lookup"><span data-stu-id="93b27-128">The site name and user name of your Eloqua account in the form: `SiteName\Username` e.g. `Eloqua\Alice`.</span></span>  | <span data-ttu-id="93b27-129">Yes</span><span class="sxs-lookup"><span data-stu-id="93b27-129">Yes</span></span> |
| <span data-ttu-id="93b27-130">password</span><span class="sxs-lookup"><span data-stu-id="93b27-130">password</span></span> | <span data-ttu-id="93b27-131">The password corresponding to the user name.</span><span class="sxs-lookup"><span data-stu-id="93b27-131">The password corresponding to the user name.</span></span> <span data-ttu-id="93b27-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="93b27-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="93b27-133">Yes</span><span class="sxs-lookup"><span data-stu-id="93b27-133">Yes</span></span> |
| <span data-ttu-id="93b27-134">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="93b27-134">useEncryptedEndpoints</span></span> | <span data-ttu-id="93b27-135">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="93b27-135">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="93b27-136">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="93b27-136">The default value is true.</span></span>  | <span data-ttu-id="93b27-137">No</span><span class="sxs-lookup"><span data-stu-id="93b27-137">No</span></span> |
| <span data-ttu-id="93b27-138">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="93b27-138">useHostVerification</span></span> | <span data-ttu-id="93b27-139">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="93b27-139">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="93b27-140">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="93b27-140">The default value is true.</span></span>  | <span data-ttu-id="93b27-141">No</span><span class="sxs-lookup"><span data-stu-id="93b27-141">No</span></span> |
| <span data-ttu-id="93b27-142">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="93b27-142">usePeerVerification</span></span> | <span data-ttu-id="93b27-143">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="93b27-143">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="93b27-144">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="93b27-144">The default value is true.</span></span>  | <span data-ttu-id="93b27-145">No</span><span class="sxs-lookup"><span data-stu-id="93b27-145">No</span></span> |

<span data-ttu-id="93b27-146">**Example:**</span><span class="sxs-lookup"><span data-stu-id="93b27-146">**Example:**</span></span>

```json
{
    "name": "EloquaLinkedService",
    "properties": {
        "type": "Eloqua",
        "typeProperties": {
            "endpoint" : "<base URL e.g. xxx.xxx.eloqua.com>",
            "username" : "<site name>\\<user name e.g. Eloqua\\Alice>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="93b27-147">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="93b27-147">Dataset properties</span></span>

<span data-ttu-id="93b27-148">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="93b27-148">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="93b27-149">This section provides a list of properties supported by Oracle Eloqua dataset.</span><span class="sxs-lookup"><span data-stu-id="93b27-149">This section provides a list of properties supported by Oracle Eloqua dataset.</span></span>

<span data-ttu-id="93b27-150">To copy data from Oracle Eloqua, set the type property of the dataset to **EloquaObject**.</span><span class="sxs-lookup"><span data-stu-id="93b27-150">To copy data from Oracle Eloqua, set the type property of the dataset to **EloquaObject**.</span></span> <span data-ttu-id="93b27-151">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="93b27-151">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="93b27-152">**Example**</span><span class="sxs-lookup"><span data-stu-id="93b27-152">**Example**</span></span>

```json
{
    "name": "EloquaDataset",
    "properties": {
        "type": "EloquaObject",
        "linkedServiceName": {
            "referenceName": "<Eloqua linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="93b27-153">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="93b27-153">Copy activity properties</span></span>

<span data-ttu-id="93b27-154">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="93b27-154">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="93b27-155">This section provides a list of properties supported by Oracle Eloqua source.</span><span class="sxs-lookup"><span data-stu-id="93b27-155">This section provides a list of properties supported by Oracle Eloqua source.</span></span>

### <a name="eloquasource-as-source"></a><span data-ttu-id="93b27-156">EloquaSource as source</span><span class="sxs-lookup"><span data-stu-id="93b27-156">EloquaSource as source</span></span>

<span data-ttu-id="93b27-157">To copy data from Oracle Eloqua, set the source type in the copy activity to **EloquaSource**.</span><span class="sxs-lookup"><span data-stu-id="93b27-157">To copy data from Oracle Eloqua, set the source type in the copy activity to **EloquaSource**.</span></span> <span data-ttu-id="93b27-158">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="93b27-158">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="93b27-159">Property</span><span class="sxs-lookup"><span data-stu-id="93b27-159">Property</span></span> | <span data-ttu-id="93b27-160">Description</span><span class="sxs-lookup"><span data-stu-id="93b27-160">Description</span></span> | <span data-ttu-id="93b27-161">Required</span><span class="sxs-lookup"><span data-stu-id="93b27-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="93b27-162">type</span><span class="sxs-lookup"><span data-stu-id="93b27-162">type</span></span> | <span data-ttu-id="93b27-163">The type property of the copy activity source must be set to: **EloquaSource**</span><span class="sxs-lookup"><span data-stu-id="93b27-163">The type property of the copy activity source must be set to: **EloquaSource**</span></span> | <span data-ttu-id="93b27-164">Yes</span><span class="sxs-lookup"><span data-stu-id="93b27-164">Yes</span></span> |
| <span data-ttu-id="93b27-165">query</span><span class="sxs-lookup"><span data-stu-id="93b27-165">query</span></span> | <span data-ttu-id="93b27-166">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="93b27-166">Use the custom SQL query to read data.</span></span> <span data-ttu-id="93b27-167">For example: `"SELECT * FROM Accounts"`.</span><span class="sxs-lookup"><span data-stu-id="93b27-167">For example: `"SELECT * FROM Accounts"`.</span></span> | <span data-ttu-id="93b27-168">Yes</span><span class="sxs-lookup"><span data-stu-id="93b27-168">Yes</span></span> |

<span data-ttu-id="93b27-169">**Example:**</span><span class="sxs-lookup"><span data-stu-id="93b27-169">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromEloqua",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Eloqua input dataset name>",
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
                "type": "EloquaSource",
                "query": "SELECT * FROM Accounts"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="93b27-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="93b27-170">Next steps</span></span>
<span data-ttu-id="93b27-171">For a list of supported data stored by Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="93b27-171">For a list of supported data stored by Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
