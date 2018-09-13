---
title: Copy data from Salesforce Marketing Cloud using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Salesforce Marketing Cloud to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: a68090ea32c7ba4155aa5474067c5cce6f1ee30b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966954"
---
# <a name="copy-data-from-salesforce-marketing-cloud-using-azure-data-factory"></a><span data-ttu-id="739fb-103">Copy data from Salesforce Marketing Cloud using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="739fb-103">Copy data from Salesforce Marketing Cloud using Azure Data Factory</span></span>

<span data-ttu-id="739fb-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Salesforce Marketing Cloud.</span><span class="sxs-lookup"><span data-stu-id="739fb-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Salesforce Marketing Cloud.</span></span> <span data-ttu-id="739fb-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="739fb-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="739fb-106">This connector is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="739fb-106">This connector is currently in preview.</span></span> <span data-ttu-id="739fb-107">You can try it out and give us feedback.</span><span class="sxs-lookup"><span data-stu-id="739fb-107">You can try it out and give us feedback.</span></span> <span data-ttu-id="739fb-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span><span class="sxs-lookup"><span data-stu-id="739fb-108">If you want to take a dependency on preview connectors in your solution, please contact [Azure support](https://azure.microsoft.com/support/).</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="739fb-109">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="739fb-109">Supported capabilities</span></span>

<span data-ttu-id="739fb-110">You can copy data from Salesforce Marketing Cloud to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="739fb-110">You can copy data from Salesforce Marketing Cloud to any supported sink data store.</span></span> <span data-ttu-id="739fb-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="739fb-111">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="739fb-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="739fb-112">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="739fb-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="739fb-113">Getting started</span></span>

<span data-ttu-id="739fb-114">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="739fb-114">You can create a pipeline with copy activity using .NET SDK, Python SDK, Azure PowerShell, REST API, or Azure Resource Manager template.</span></span> <span data-ttu-id="739fb-115">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="739fb-115">See [Copy activity tutorial](quickstart-create-data-factory-dot-net.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="739fb-116">The following sections provide details about properties that are used to define Data Factory entities specific to Salesforce Marketing Cloud connector.</span><span class="sxs-lookup"><span data-stu-id="739fb-116">The following sections provide details about properties that are used to define Data Factory entities specific to Salesforce Marketing Cloud connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="739fb-117">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="739fb-117">Linked service properties</span></span>

<span data-ttu-id="739fb-118">The following properties are supported for Salesforce Marketing Cloud linked service:</span><span class="sxs-lookup"><span data-stu-id="739fb-118">The following properties are supported for Salesforce Marketing Cloud linked service:</span></span>

| <span data-ttu-id="739fb-119">Property</span><span class="sxs-lookup"><span data-stu-id="739fb-119">Property</span></span> | <span data-ttu-id="739fb-120">Description</span><span class="sxs-lookup"><span data-stu-id="739fb-120">Description</span></span> | <span data-ttu-id="739fb-121">Required</span><span class="sxs-lookup"><span data-stu-id="739fb-121">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="739fb-122">type</span><span class="sxs-lookup"><span data-stu-id="739fb-122">type</span></span> | <span data-ttu-id="739fb-123">The type property must be set to: **SalesforceMarketingCloud**</span><span class="sxs-lookup"><span data-stu-id="739fb-123">The type property must be set to: **SalesforceMarketingCloud**</span></span> | <span data-ttu-id="739fb-124">Yes</span><span class="sxs-lookup"><span data-stu-id="739fb-124">Yes</span></span> |
| <span data-ttu-id="739fb-125">clientId</span><span class="sxs-lookup"><span data-stu-id="739fb-125">clientId</span></span> | <span data-ttu-id="739fb-126">The client ID associated with the Salesforce Marketing Cloud application.</span><span class="sxs-lookup"><span data-stu-id="739fb-126">The client ID associated with the Salesforce Marketing Cloud application.</span></span>  | <span data-ttu-id="739fb-127">Yes</span><span class="sxs-lookup"><span data-stu-id="739fb-127">Yes</span></span> |
| <span data-ttu-id="739fb-128">clientSecret</span><span class="sxs-lookup"><span data-stu-id="739fb-128">clientSecret</span></span> | <span data-ttu-id="739fb-129">The client secret associated with the Salesforce Marketing Cloud application.</span><span class="sxs-lookup"><span data-stu-id="739fb-129">The client secret associated with the Salesforce Marketing Cloud application.</span></span> <span data-ttu-id="739fb-130">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="739fb-130">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let ADF copy acitivty pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="739fb-131">Yes</span><span class="sxs-lookup"><span data-stu-id="739fb-131">Yes</span></span> |
| <span data-ttu-id="739fb-132">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="739fb-132">useEncryptedEndpoints</span></span> | <span data-ttu-id="739fb-133">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="739fb-133">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="739fb-134">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="739fb-134">The default value is true.</span></span>  | <span data-ttu-id="739fb-135">No</span><span class="sxs-lookup"><span data-stu-id="739fb-135">No</span></span> |
| <span data-ttu-id="739fb-136">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="739fb-136">useHostVerification</span></span> | <span data-ttu-id="739fb-137">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="739fb-137">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="739fb-138">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="739fb-138">The default value is true.</span></span>  | <span data-ttu-id="739fb-139">No</span><span class="sxs-lookup"><span data-stu-id="739fb-139">No</span></span> |
| <span data-ttu-id="739fb-140">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="739fb-140">usePeerVerification</span></span> | <span data-ttu-id="739fb-141">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="739fb-141">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="739fb-142">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="739fb-142">The default value is true.</span></span>  | <span data-ttu-id="739fb-143">No</span><span class="sxs-lookup"><span data-stu-id="739fb-143">No</span></span> |

<span data-ttu-id="739fb-144">**Example:**</span><span class="sxs-lookup"><span data-stu-id="739fb-144">**Example:**</span></span>

```json
{
    "name": "SalesforceMarketingCloudLinkedService",
    "properties": {
        "type": "SalesforceMarketingCloud",
        "typeProperties": {
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

## <a name="dataset-properties"></a><span data-ttu-id="739fb-145">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="739fb-145">Dataset properties</span></span>

<span data-ttu-id="739fb-146">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="739fb-146">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="739fb-147">This section provides a list of properties supported by Salesforce Marketing Cloud dataset.</span><span class="sxs-lookup"><span data-stu-id="739fb-147">This section provides a list of properties supported by Salesforce Marketing Cloud dataset.</span></span>

<span data-ttu-id="739fb-148">To copy data from Salesforce Marketing Cloud, set the type property of the dataset to **SalesforceMarketingCloudObject**.</span><span class="sxs-lookup"><span data-stu-id="739fb-148">To copy data from Salesforce Marketing Cloud, set the type property of the dataset to **SalesforceMarketingCloudObject**.</span></span> <span data-ttu-id="739fb-149">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="739fb-149">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="739fb-150">**Example**</span><span class="sxs-lookup"><span data-stu-id="739fb-150">**Example**</span></span>

```json
{
    "name": "SalesforceMarketingCloudDataset",
    "properties": {
        "type": "SalesforceMarketingCloudObject",
        "linkedServiceName": {
            "referenceName": "<SalesforceMarketingCloud linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="739fb-151">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="739fb-151">Copy activity properties</span></span>

<span data-ttu-id="739fb-152">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="739fb-152">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="739fb-153">This section provides a list of properties supported by Salesforce Marketing Cloud source.</span><span class="sxs-lookup"><span data-stu-id="739fb-153">This section provides a list of properties supported by Salesforce Marketing Cloud source.</span></span>

### <a name="salesforce-marketing-cloud-as-source"></a><span data-ttu-id="739fb-154">Salesforce Marketing Cloud as source</span><span class="sxs-lookup"><span data-stu-id="739fb-154">Salesforce Marketing Cloud as source</span></span>

<span data-ttu-id="739fb-155">To copy data from Salesforce Marketing Cloud, set the source type in the copy activity to **SalesforceMarketingCloudSource**.</span><span class="sxs-lookup"><span data-stu-id="739fb-155">To copy data from Salesforce Marketing Cloud, set the source type in the copy activity to **SalesforceMarketingCloudSource**.</span></span> <span data-ttu-id="739fb-156">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="739fb-156">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="739fb-157">Property</span><span class="sxs-lookup"><span data-stu-id="739fb-157">Property</span></span> | <span data-ttu-id="739fb-158">Description</span><span class="sxs-lookup"><span data-stu-id="739fb-158">Description</span></span> | <span data-ttu-id="739fb-159">Required</span><span class="sxs-lookup"><span data-stu-id="739fb-159">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="739fb-160">type</span><span class="sxs-lookup"><span data-stu-id="739fb-160">type</span></span> | <span data-ttu-id="739fb-161">The type property of the copy activity source must be set to: **SalesforceMarketingCloudSource**</span><span class="sxs-lookup"><span data-stu-id="739fb-161">The type property of the copy activity source must be set to: **SalesforceMarketingCloudSource**</span></span> | <span data-ttu-id="739fb-162">Yes</span><span class="sxs-lookup"><span data-stu-id="739fb-162">Yes</span></span> |
| <span data-ttu-id="739fb-163">query</span><span class="sxs-lookup"><span data-stu-id="739fb-163">query</span></span> | <span data-ttu-id="739fb-164">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="739fb-164">Use the custom SQL query to read data.</span></span> <span data-ttu-id="739fb-165">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="739fb-165">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="739fb-166">Yes</span><span class="sxs-lookup"><span data-stu-id="739fb-166">Yes</span></span> |

<span data-ttu-id="739fb-167">**Example:**</span><span class="sxs-lookup"><span data-stu-id="739fb-167">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSalesforceMarketingCloud",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SalesforceMarketingCloud input dataset name>",
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
                "type": "SalesforceMarketingCloudSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="739fb-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="739fb-168">Next steps</span></span>
<span data-ttu-id="739fb-169">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="739fb-169">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
