---
title: Copy data from Oracle Responsys using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Oracle Responsys to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 1368a75fb8ae44949ef25def19589ab164e25d8b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870921"
---
# <a name="copy-data-from-oracle-responsys-using-azure-data-factory"></a><span data-ttu-id="6be76-103">Copy data from Oracle Responsys using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6be76-103">Copy data from Oracle Responsys using Azure Data Factory</span></span>

<span data-ttu-id="6be76-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Oracle Responsys.</span><span class="sxs-lookup"><span data-stu-id="6be76-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Oracle Responsys.</span></span> <span data-ttu-id="6be76-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="6be76-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6be76-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="6be76-106">This connector is currently in preview.</span></span> <span data-ttu-id="6be76-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="6be76-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="6be76-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="6be76-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="6be76-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="6be76-109">Supported capabilities</span></span>

<span data-ttu-id="6be76-110">You can copy data from Oracle Responsys to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="6be76-110">You can copy data from Oracle Responsys to any supported sink data store.</span></span> <span data-ttu-id="6be76-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="6be76-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="6be76-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="6be76-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6be76-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="6be76-113">Getting started</span></span>

<span data-ttu-id="6be76-114">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="6be76-114">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span></span> <span data-ttu-id="6be76-115">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="6be76-115">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="6be76-116">The following sections provide details about properties that are used to define Data Factory entities specific to Oracle Responsys connector.</span><span class="sxs-lookup"><span data-stu-id="6be76-116">The following sections provide details about properties that are used to define Data Factory entities specific to Oracle Responsys connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6be76-117">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="6be76-117">Linked service properties</span></span>

<span data-ttu-id="6be76-118">The following properties are supported for Oracle Responsys linked service:</span><span class="sxs-lookup"><span data-stu-id="6be76-118">The following properties are supported for Oracle Responsys linked service:</span></span>

| <span data-ttu-id="6be76-119">Property</span><span class="sxs-lookup"><span data-stu-id="6be76-119">Property</span></span> | <span data-ttu-id="6be76-120">Description</span><span class="sxs-lookup"><span data-stu-id="6be76-120">Description</span></span> | <span data-ttu-id="6be76-121">Required</span><span class="sxs-lookup"><span data-stu-id="6be76-121">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6be76-122">type</span><span class="sxs-lookup"><span data-stu-id="6be76-122">type</span></span> | <span data-ttu-id="6be76-123">The type property must be set to: **Responsys**</span><span class="sxs-lookup"><span data-stu-id="6be76-123">The type property must be set to: **Responsys**</span></span> | <span data-ttu-id="6be76-124">Yes</span><span class="sxs-lookup"><span data-stu-id="6be76-124">Yes</span></span> |
| <span data-ttu-id="6be76-125">endpoint</span><span class="sxs-lookup"><span data-stu-id="6be76-125">endpoint</span></span> | <span data-ttu-id="6be76-126">The endpoint of the Respopnsys server</span><span class="sxs-lookup"><span data-stu-id="6be76-126">The endpoint of the Respopnsys server</span></span>  | <span data-ttu-id="6be76-127">Yes</span><span class="sxs-lookup"><span data-stu-id="6be76-127">Yes</span></span> |
| <span data-ttu-id="6be76-128">clientId</span><span class="sxs-lookup"><span data-stu-id="6be76-128">clientId</span></span> | <span data-ttu-id="6be76-129">The client ID associated with the Responsys application.</span><span class="sxs-lookup"><span data-stu-id="6be76-129">The client ID associated with the Responsys application.</span></span>  | <span data-ttu-id="6be76-130">Yes</span><span class="sxs-lookup"><span data-stu-id="6be76-130">Yes</span></span> |
| <span data-ttu-id="6be76-131">clientSecret</span><span class="sxs-lookup"><span data-stu-id="6be76-131">clientSecret</span></span> | <span data-ttu-id="6be76-132">The client secret associated with the Responsys application.</span><span class="sxs-lookup"><span data-stu-id="6be76-132">The client secret associated with the Responsys application.</span></span> <span data-ttu-id="6be76-133">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="6be76-133">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="6be76-134">Yes</span><span class="sxs-lookup"><span data-stu-id="6be76-134">Yes</span></span> |
| <span data-ttu-id="6be76-135">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="6be76-135">useEncryptedEndpoints</span></span> | <span data-ttu-id="6be76-136">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6be76-136">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="6be76-137">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="6be76-137">The default value is true.</span></span>  | <span data-ttu-id="6be76-138">No</span><span class="sxs-lookup"><span data-stu-id="6be76-138">No</span></span> |
| <span data-ttu-id="6be76-139">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="6be76-139">useHostVerification</span></span> | <span data-ttu-id="6be76-140">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="6be76-140">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="6be76-141">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="6be76-141">The default value is true.</span></span>  | <span data-ttu-id="6be76-142">No</span><span class="sxs-lookup"><span data-stu-id="6be76-142">No</span></span> |
| <span data-ttu-id="6be76-143">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="6be76-143">usePeerVerification</span></span> | <span data-ttu-id="6be76-144">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="6be76-144">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="6be76-145">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="6be76-145">The default value is true.</span></span>  | <span data-ttu-id="6be76-146">No</span><span class="sxs-lookup"><span data-stu-id="6be76-146">No</span></span> |

<span data-ttu-id="6be76-147">**Example:**</span><span class="sxs-lookup"><span data-stu-id="6be76-147">**Example:**</span></span>

```json
{
    "name": "OracleResponsysLinkedService",
    "properties": {
        "type": "Responsys",
        "typeProperties": {
            "endpoint" : "<endpoint>",
            "clientId" : "<clientId>",
            "clientSecret": {
                 "type": "SecureString",
                 "value": "<clientSecret>"
            },
            "useEncryptedEndpoints" : true,
            "useHostVerification" : true,
            "usePeerVerification" : true
        }
    }
}

```

## <a name="dataset-properties"></a><span data-ttu-id="6be76-148">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="6be76-148">Dataset properties</span></span>

<span data-ttu-id="6be76-149">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="6be76-149">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="6be76-150">This section provides a list of properties supported by Oracle Responsys dataset.</span><span class="sxs-lookup"><span data-stu-id="6be76-150">This section provides a list of properties supported by Oracle Responsys dataset.</span></span>

<span data-ttu-id="6be76-151">To copy data from Oracle Responsys, set the type property of the dataset to **ResponsysObject**.</span><span class="sxs-lookup"><span data-stu-id="6be76-151">To copy data from Oracle Responsys, set the type property of the dataset to **ResponsysObject**.</span></span> <span data-ttu-id="6be76-152">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="6be76-152">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="6be76-153">**Example**</span><span class="sxs-lookup"><span data-stu-id="6be76-153">**Example**</span></span>

```json
{
    "name": "OracleResponsysDataset",
    "properties": {
        "type": "ResponsysObject",
        "linkedServiceName": {
            "referenceName": "<Oracle Responsys linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}

```

## <a name="copy-activity-properties"></a><span data-ttu-id="6be76-154">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="6be76-154">Copy activity properties</span></span>

<span data-ttu-id="6be76-155">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="6be76-155">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="6be76-156">This section provides a list of properties supported by Oracle Responsys source.</span><span class="sxs-lookup"><span data-stu-id="6be76-156">This section provides a list of properties supported by Oracle Responsys source.</span></span>

### <a name="oracle-responsys-as-source"></a><span data-ttu-id="6be76-157">Oracle Responsys as source</span><span class="sxs-lookup"><span data-stu-id="6be76-157">Oracle Responsys as source</span></span>

<span data-ttu-id="6be76-158">To copy data from Oracle Responsys, set the source type in the copy activity to **ResponsysSource**.</span><span class="sxs-lookup"><span data-stu-id="6be76-158">To copy data from Oracle Responsys, set the source type in the copy activity to **ResponsysSource**.</span></span> <span data-ttu-id="6be76-159">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="6be76-159">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="6be76-160">Property</span><span class="sxs-lookup"><span data-stu-id="6be76-160">Property</span></span> | <span data-ttu-id="6be76-161">Description</span><span class="sxs-lookup"><span data-stu-id="6be76-161">Description</span></span> | <span data-ttu-id="6be76-162">Required</span><span class="sxs-lookup"><span data-stu-id="6be76-162">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6be76-163">type</span><span class="sxs-lookup"><span data-stu-id="6be76-163">type</span></span> | <span data-ttu-id="6be76-164">The type property of the copy activity source must be set to: **ResponsysSource**</span><span class="sxs-lookup"><span data-stu-id="6be76-164">The type property of the copy activity source must be set to: **ResponsysSource**</span></span> | <span data-ttu-id="6be76-165">Yes</span><span class="sxs-lookup"><span data-stu-id="6be76-165">Yes</span></span> |
| <span data-ttu-id="6be76-166">query</span><span class="sxs-lookup"><span data-stu-id="6be76-166">query</span></span> | <span data-ttu-id="6be76-167">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="6be76-167">Use the custom SQL query to read data.</span></span> <span data-ttu-id="6be76-168">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="6be76-168">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="6be76-169">Yes</span><span class="sxs-lookup"><span data-stu-id="6be76-169">Yes</span></span> |

<span data-ttu-id="6be76-170">**Example:**</span><span class="sxs-lookup"><span data-stu-id="6be76-170">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromOracleResponsys",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Oracle Responsys input dataset name>",
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
                "type": "ResponsysSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="6be76-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="6be76-171">Next steps</span></span>
<span data-ttu-id="6be76-172">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6be76-172">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
