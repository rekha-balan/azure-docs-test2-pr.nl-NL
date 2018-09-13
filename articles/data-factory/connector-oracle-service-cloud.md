---
title: Copy data from Oracle Service Cloud using Azure Data Factory (Preview) | Microsoft Docs
description: Learn how to copy data from Oracle Service Cloud to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 09/07/2018
ms.author: jingwang
ms.openlocfilehash: a576b94881e114a97e58bf93515e372221da3346
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869525"
---
# <a name="copy-data-from-oracle-service-cloud-using-azure-data-factory-preview"></a><span data-ttu-id="e1bc2-103">Copy data from Oracle Service Cloud using Azure Data Factory (Preview)</span><span class="sxs-lookup"><span data-stu-id="e1bc2-103">Copy data from Oracle Service Cloud using Azure Data Factory (Preview)</span></span>

<span data-ttu-id="e1bc2-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Oracle Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Oracle Service Cloud.</span></span> <span data-ttu-id="e1bc2-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1bc2-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-106">This connector is currently in preview.</span></span> <span data-ttu-id="e1bc2-107">You can try it out and provide feedback.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-107">You can try it out and provide feedback.</span></span> <span data-ttu-id="e1bc2-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="e1bc2-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="e1bc2-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="e1bc2-109">Supported capabilities</span></span>

<span data-ttu-id="e1bc2-110">You can copy data from Oracle Service Cloud to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-110">You can copy data from Oracle Service Cloud to any supported sink data store.</span></span> <span data-ttu-id="e1bc2-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="e1bc2-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e1bc2-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="e1bc2-113">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="e1bc2-114">The following sections provide details about properties that are used to define Data Factory entities specific to Oracle Service Cloud connector.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-114">The following sections provide details about properties that are used to define Data Factory entities specific to Oracle Service Cloud connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e1bc2-115">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="e1bc2-115">Linked service properties</span></span>

<span data-ttu-id="e1bc2-116">The following properties are supported for Oracle Service Cloud linked service:</span><span class="sxs-lookup"><span data-stu-id="e1bc2-116">The following properties are supported for Oracle Service Cloud linked service:</span></span>

| <span data-ttu-id="e1bc2-117">Property</span><span class="sxs-lookup"><span data-stu-id="e1bc2-117">Property</span></span> | <span data-ttu-id="e1bc2-118">Description</span><span class="sxs-lookup"><span data-stu-id="e1bc2-118">Description</span></span> | <span data-ttu-id="e1bc2-119">Required</span><span class="sxs-lookup"><span data-stu-id="e1bc2-119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e1bc2-120">type</span><span class="sxs-lookup"><span data-stu-id="e1bc2-120">type</span></span> | <span data-ttu-id="e1bc2-121">The type property must be set to: **OracleServiceCloud**</span><span class="sxs-lookup"><span data-stu-id="e1bc2-121">The type property must be set to: **OracleServiceCloud**</span></span> | <span data-ttu-id="e1bc2-122">Yes</span><span class="sxs-lookup"><span data-stu-id="e1bc2-122">Yes</span></span> |
| <span data-ttu-id="e1bc2-123">host</span><span class="sxs-lookup"><span data-stu-id="e1bc2-123">host</span></span> | <span data-ttu-id="e1bc2-124">The URL of the Oracle Service Cloud instance.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-124">The URL of the Oracle Service Cloud instance.</span></span>  | <span data-ttu-id="e1bc2-125">Yes</span><span class="sxs-lookup"><span data-stu-id="e1bc2-125">Yes</span></span> |
| <span data-ttu-id="e1bc2-126">username</span><span class="sxs-lookup"><span data-stu-id="e1bc2-126">username</span></span> | <span data-ttu-id="e1bc2-127">The user name that you use to access Oracle Service Cloud server.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-127">The user name that you use to access Oracle Service Cloud server.</span></span>  | <span data-ttu-id="e1bc2-128">Yes</span><span class="sxs-lookup"><span data-stu-id="e1bc2-128">Yes</span></span> |
| <span data-ttu-id="e1bc2-129">password</span><span class="sxs-lookup"><span data-stu-id="e1bc2-129">password</span></span> | <span data-ttu-id="e1bc2-130">The password corresponding to the user name that you provided in the username key.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-130">The password corresponding to the user name that you provided in the username key.</span></span> <span data-ttu-id="e1bc2-131">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e1bc2-131">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="e1bc2-132">Yes</span><span class="sxs-lookup"><span data-stu-id="e1bc2-132">Yes</span></span> |
| <span data-ttu-id="e1bc2-133">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="e1bc2-133">useEncryptedEndpoints</span></span> | <span data-ttu-id="e1bc2-134">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-134">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="e1bc2-135">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-135">The default value is true.</span></span>  | <span data-ttu-id="e1bc2-136">No</span><span class="sxs-lookup"><span data-stu-id="e1bc2-136">No</span></span> |
| <span data-ttu-id="e1bc2-137">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="e1bc2-137">useHostVerification</span></span> | <span data-ttu-id="e1bc2-138">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-138">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="e1bc2-139">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-139">The default value is true.</span></span>  | <span data-ttu-id="e1bc2-140">No</span><span class="sxs-lookup"><span data-stu-id="e1bc2-140">No</span></span> |
| <span data-ttu-id="e1bc2-141">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="e1bc2-141">usePeerVerification</span></span> | <span data-ttu-id="e1bc2-142">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-142">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="e1bc2-143">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-143">The default value is true.</span></span>  | <span data-ttu-id="e1bc2-144">No</span><span class="sxs-lookup"><span data-stu-id="e1bc2-144">No</span></span> |

<span data-ttu-id="e1bc2-145">**Example:**</span><span class="sxs-lookup"><span data-stu-id="e1bc2-145">**Example:**</span></span>

```json
{
    "name": "OracleServiceCloudLinkedService",
    "properties": {
        "type": "OracleServiceCloud",
        "typeProperties": {
            "host" : "<host>",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            },
            "useEncryptedEndpoints" : true,
            "useHostVerification" : true,
            "usePeerVerification" : true,
        }
    }
}

```

## <a name="dataset-properties"></a><span data-ttu-id="e1bc2-146">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="e1bc2-146">Dataset properties</span></span>

<span data-ttu-id="e1bc2-147">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-147">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="e1bc2-148">This section provides a list of properties supported by Oracle Service Cloud dataset.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-148">This section provides a list of properties supported by Oracle Service Cloud dataset.</span></span>

<span data-ttu-id="e1bc2-149">To copy data from Oracle Service Cloud, set the type property of the dataset to **OracleServiceCloudObject**.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-149">To copy data from Oracle Service Cloud, set the type property of the dataset to **OracleServiceCloudObject**.</span></span> <span data-ttu-id="e1bc2-150">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-150">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="e1bc2-151">**Example**</span><span class="sxs-lookup"><span data-stu-id="e1bc2-151">**Example**</span></span>

```json
{
    "name": "OracleServiceCloudDataset",
    "properties": {
        "type": "OracleServiceCloudObject",
        "linkedServiceName": {
            "referenceName": "<OracleServiceCloud linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}

```

## <a name="copy-activity-properties"></a><span data-ttu-id="e1bc2-152">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="e1bc2-152">Copy activity properties</span></span>

<span data-ttu-id="e1bc2-153">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-153">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="e1bc2-154">This section provides a list of properties supported by Oracle Service Cloud source.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-154">This section provides a list of properties supported by Oracle Service Cloud source.</span></span>

### <a name="oracle-service-cloud-as-source"></a><span data-ttu-id="e1bc2-155">Oracle Service Cloud as source</span><span class="sxs-lookup"><span data-stu-id="e1bc2-155">Oracle Service Cloud as source</span></span>

<span data-ttu-id="e1bc2-156">To copy data from Oracle Service Cloud, set the source type in the copy activity to **OracleServiceCloudSource**.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-156">To copy data from Oracle Service Cloud, set the source type in the copy activity to **OracleServiceCloudSource**.</span></span> <span data-ttu-id="e1bc2-157">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="e1bc2-157">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="e1bc2-158">Property</span><span class="sxs-lookup"><span data-stu-id="e1bc2-158">Property</span></span> | <span data-ttu-id="e1bc2-159">Description</span><span class="sxs-lookup"><span data-stu-id="e1bc2-159">Description</span></span> | <span data-ttu-id="e1bc2-160">Required</span><span class="sxs-lookup"><span data-stu-id="e1bc2-160">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e1bc2-161">type</span><span class="sxs-lookup"><span data-stu-id="e1bc2-161">type</span></span> | <span data-ttu-id="e1bc2-162">The type property of the copy activity source must be set to: **OracleServiceCloudSource**</span><span class="sxs-lookup"><span data-stu-id="e1bc2-162">The type property of the copy activity source must be set to: **OracleServiceCloudSource**</span></span> | <span data-ttu-id="e1bc2-163">Yes</span><span class="sxs-lookup"><span data-stu-id="e1bc2-163">Yes</span></span> |
| <span data-ttu-id="e1bc2-164">query</span><span class="sxs-lookup"><span data-stu-id="e1bc2-164">query</span></span> | <span data-ttu-id="e1bc2-165">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-165">Use the custom SQL query to read data.</span></span> <span data-ttu-id="e1bc2-166">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="e1bc2-166">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="e1bc2-167">Yes</span><span class="sxs-lookup"><span data-stu-id="e1bc2-167">Yes</span></span> |

<span data-ttu-id="e1bc2-168">**Example:**</span><span class="sxs-lookup"><span data-stu-id="e1bc2-168">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromOracleServiceCloud",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<OracleServiceCloud input dataset name>",
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
                "type": "OracleServiceCloudSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="e1bc2-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1bc2-169">Next steps</span></span>
<span data-ttu-id="e1bc2-170">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="e1bc2-170">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
