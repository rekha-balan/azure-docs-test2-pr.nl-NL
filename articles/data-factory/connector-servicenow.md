---
title: Copy data from ServiceNow using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from ServiceNow to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 05/28/2018
ms.author: jingwang
ms.openlocfilehash: c67f6c14dc396367e0179fe5bdb4663fcb7725da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866895"
---
# <a name="copy-data-from-servicenow-using-azure-data-factory"></a><span data-ttu-id="54141-103">Copy data from ServiceNow using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="54141-103">Copy data from ServiceNow using Azure Data Factory</span></span>

<span data-ttu-id="54141-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="54141-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from ServiceNow.</span></span> <span data-ttu-id="54141-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="54141-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="54141-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="54141-106">Supported capabilities</span></span>

<span data-ttu-id="54141-107">You can copy data from ServiceNow to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="54141-107">You can copy data from ServiceNow to any supported sink data store.</span></span> <span data-ttu-id="54141-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="54141-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="54141-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="54141-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="54141-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="54141-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="54141-111">The following sections provide details about properties that are used to define Data Factory entities specific to ServiceNow connector.</span><span class="sxs-lookup"><span data-stu-id="54141-111">The following sections provide details about properties that are used to define Data Factory entities specific to ServiceNow connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="54141-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="54141-112">Linked service properties</span></span>

<span data-ttu-id="54141-113">The following properties are supported for ServiceNow linked service:</span><span class="sxs-lookup"><span data-stu-id="54141-113">The following properties are supported for ServiceNow linked service:</span></span>

| <span data-ttu-id="54141-114">Property</span><span class="sxs-lookup"><span data-stu-id="54141-114">Property</span></span> | <span data-ttu-id="54141-115">Description</span><span class="sxs-lookup"><span data-stu-id="54141-115">Description</span></span> | <span data-ttu-id="54141-116">Required</span><span class="sxs-lookup"><span data-stu-id="54141-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54141-117">type</span><span class="sxs-lookup"><span data-stu-id="54141-117">type</span></span> | <span data-ttu-id="54141-118">The type property must be set to: **ServiceNow**</span><span class="sxs-lookup"><span data-stu-id="54141-118">The type property must be set to: **ServiceNow**</span></span> | <span data-ttu-id="54141-119">Yes</span><span class="sxs-lookup"><span data-stu-id="54141-119">Yes</span></span> |
| <span data-ttu-id="54141-120">endpoint</span><span class="sxs-lookup"><span data-stu-id="54141-120">endpoint</span></span> | <span data-ttu-id="54141-121">The endpoint of the ServiceNow server (`http://<instance>.service-now.com`).</span><span class="sxs-lookup"><span data-stu-id="54141-121">The endpoint of the ServiceNow server (`http://<instance>.service-now.com`).</span></span>  | <span data-ttu-id="54141-122">Yes</span><span class="sxs-lookup"><span data-stu-id="54141-122">Yes</span></span> |
| <span data-ttu-id="54141-123">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54141-123">authenticationType</span></span> | <span data-ttu-id="54141-124">The authentication type to use.</span><span class="sxs-lookup"><span data-stu-id="54141-124">The authentication type to use.</span></span> <br/><span data-ttu-id="54141-125">Allowed values are: **Basic**, **OAuth2**</span><span class="sxs-lookup"><span data-stu-id="54141-125">Allowed values are: **Basic**, **OAuth2**</span></span> | <span data-ttu-id="54141-126">Yes</span><span class="sxs-lookup"><span data-stu-id="54141-126">Yes</span></span> |
| <span data-ttu-id="54141-127">username</span><span class="sxs-lookup"><span data-stu-id="54141-127">username</span></span> | <span data-ttu-id="54141-128">The user name used to connect to the ServiceNow server for Basic and OAuth2 authentication.</span><span class="sxs-lookup"><span data-stu-id="54141-128">The user name used to connect to the ServiceNow server for Basic and OAuth2 authentication.</span></span>  | <span data-ttu-id="54141-129">Yes</span><span class="sxs-lookup"><span data-stu-id="54141-129">Yes</span></span> |
| <span data-ttu-id="54141-130">password</span><span class="sxs-lookup"><span data-stu-id="54141-130">password</span></span> | <span data-ttu-id="54141-131">The password corresponding to the user name for Basic and OAuth2 authentication.</span><span class="sxs-lookup"><span data-stu-id="54141-131">The password corresponding to the user name for Basic and OAuth2 authentication.</span></span> <span data-ttu-id="54141-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="54141-132">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="54141-133">Yes</span><span class="sxs-lookup"><span data-stu-id="54141-133">Yes</span></span> |
| <span data-ttu-id="54141-134">clientId</span><span class="sxs-lookup"><span data-stu-id="54141-134">clientId</span></span> | <span data-ttu-id="54141-135">The client ID for OAuth2 authentication.</span><span class="sxs-lookup"><span data-stu-id="54141-135">The client ID for OAuth2 authentication.</span></span>  | <span data-ttu-id="54141-136">No</span><span class="sxs-lookup"><span data-stu-id="54141-136">No</span></span> |
| <span data-ttu-id="54141-137">clientSecret</span><span class="sxs-lookup"><span data-stu-id="54141-137">clientSecret</span></span> | <span data-ttu-id="54141-138">The client secret for OAuth2 authentication.</span><span class="sxs-lookup"><span data-stu-id="54141-138">The client secret for OAuth2 authentication.</span></span> <span data-ttu-id="54141-139">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="54141-139">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="54141-140">No</span><span class="sxs-lookup"><span data-stu-id="54141-140">No</span></span> |
| <span data-ttu-id="54141-141">useEncryptedEndpoints</span><span class="sxs-lookup"><span data-stu-id="54141-141">useEncryptedEndpoints</span></span> | <span data-ttu-id="54141-142">Specifies whether the data source endpoints are encrypted using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="54141-142">Specifies whether the data source endpoints are encrypted using HTTPS.</span></span> <span data-ttu-id="54141-143">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="54141-143">The default value is true.</span></span>  | <span data-ttu-id="54141-144">No</span><span class="sxs-lookup"><span data-stu-id="54141-144">No</span></span> |
| <span data-ttu-id="54141-145">useHostVerification</span><span class="sxs-lookup"><span data-stu-id="54141-145">useHostVerification</span></span> | <span data-ttu-id="54141-146">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="54141-146">Specifies whether to require the host name in the server's certificate to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="54141-147">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="54141-147">The default value is true.</span></span>  | <span data-ttu-id="54141-148">No</span><span class="sxs-lookup"><span data-stu-id="54141-148">No</span></span> |
| <span data-ttu-id="54141-149">usePeerVerification</span><span class="sxs-lookup"><span data-stu-id="54141-149">usePeerVerification</span></span> | <span data-ttu-id="54141-150">Specifies whether to verify the identity of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="54141-150">Specifies whether to verify the identity of the server when connecting over SSL.</span></span> <span data-ttu-id="54141-151">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="54141-151">The default value is true.</span></span>  | <span data-ttu-id="54141-152">No</span><span class="sxs-lookup"><span data-stu-id="54141-152">No</span></span> |

<span data-ttu-id="54141-153">**Example:**</span><span class="sxs-lookup"><span data-stu-id="54141-153">**Example:**</span></span>

```json
{
    "name": "ServiceNowLinkedService",
    "properties": {
        "type": "ServiceNow",
        "typeProperties": {
            "endpoint" : "http://<instance>.service-now.com",
            "authenticationType" : "Basic",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="54141-154">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="54141-154">Dataset properties</span></span>

<span data-ttu-id="54141-155">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="54141-155">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="54141-156">This section provides a list of properties supported by ServiceNow dataset.</span><span class="sxs-lookup"><span data-stu-id="54141-156">This section provides a list of properties supported by ServiceNow dataset.</span></span>

<span data-ttu-id="54141-157">To copy data from ServiceNow, set the type property of the dataset to **ServiceNowObject**.</span><span class="sxs-lookup"><span data-stu-id="54141-157">To copy data from ServiceNow, set the type property of the dataset to **ServiceNowObject**.</span></span> <span data-ttu-id="54141-158">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="54141-158">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="54141-159">**Example**</span><span class="sxs-lookup"><span data-stu-id="54141-159">**Example**</span></span>

```json
{
    "name": "ServiceNowDataset",
    "properties": {
        "type": "ServiceNowObject",
        "linkedServiceName": {
            "referenceName": "<ServiceNow linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="54141-160">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="54141-160">Copy activity properties</span></span>

<span data-ttu-id="54141-161">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="54141-161">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="54141-162">This section provides a list of properties supported by ServiceNow source.</span><span class="sxs-lookup"><span data-stu-id="54141-162">This section provides a list of properties supported by ServiceNow source.</span></span>

### <a name="servicenow-as-source"></a><span data-ttu-id="54141-163">ServiceNow as source</span><span class="sxs-lookup"><span data-stu-id="54141-163">ServiceNow as source</span></span>

<span data-ttu-id="54141-164">To copy data from ServiceNow, set the source type in the copy activity to **ServiceNowSource**.</span><span class="sxs-lookup"><span data-stu-id="54141-164">To copy data from ServiceNow, set the source type in the copy activity to **ServiceNowSource**.</span></span> <span data-ttu-id="54141-165">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="54141-165">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="54141-166">Property</span><span class="sxs-lookup"><span data-stu-id="54141-166">Property</span></span> | <span data-ttu-id="54141-167">Description</span><span class="sxs-lookup"><span data-stu-id="54141-167">Description</span></span> | <span data-ttu-id="54141-168">Required</span><span class="sxs-lookup"><span data-stu-id="54141-168">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54141-169">type</span><span class="sxs-lookup"><span data-stu-id="54141-169">type</span></span> | <span data-ttu-id="54141-170">The type property of the copy activity source must be set to: **ServiceNowSource**</span><span class="sxs-lookup"><span data-stu-id="54141-170">The type property of the copy activity source must be set to: **ServiceNowSource**</span></span> | <span data-ttu-id="54141-171">Yes</span><span class="sxs-lookup"><span data-stu-id="54141-171">Yes</span></span> |
| <span data-ttu-id="54141-172">query</span><span class="sxs-lookup"><span data-stu-id="54141-172">query</span></span> | <span data-ttu-id="54141-173">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="54141-173">Use the custom SQL query to read data.</span></span> <span data-ttu-id="54141-174">For example: `"SELECT * FROM Actual.alm_asset"`.</span><span class="sxs-lookup"><span data-stu-id="54141-174">For example: `"SELECT * FROM Actual.alm_asset"`.</span></span> | <span data-ttu-id="54141-175">Yes</span><span class="sxs-lookup"><span data-stu-id="54141-175">Yes</span></span> |

<span data-ttu-id="54141-176">Note the following when specifying the schema and column for ServiceNow in query:</span><span class="sxs-lookup"><span data-stu-id="54141-176">Note the following when specifying the schema and column for ServiceNow in query:</span></span>

- <span data-ttu-id="54141-177">**Schema:** specify the schema as `Actual` or `Display` in the ServiceNow query, which you can look at it as the parameter of `sysparm_display_value` as true or false when calling [ServiceNow restful APIs](https://developer.servicenow.com/app.do#!/rest_api_doc?v=jakarta&id=r_AggregateAPI-GET).</span><span class="sxs-lookup"><span data-stu-id="54141-177">**Schema:** specify the schema as `Actual` or `Display` in the ServiceNow query, which you can look at it as the parameter of `sysparm_display_value` as true or false when calling [ServiceNow restful APIs](https://developer.servicenow.com/app.do#!/rest_api_doc?v=jakarta&id=r_AggregateAPI-GET).</span></span> 
- <span data-ttu-id="54141-178">**Column:** the column name for actual value under `Actual` schema is `[columne name]_value`, while for display value under `Display` schema is `[columne name]_display_value`.</span><span class="sxs-lookup"><span data-stu-id="54141-178">**Column:** the column name for actual value under `Actual` schema is `[columne name]_value`, while for display value under `Display` schema is `[columne name]_display_value`.</span></span> <span data-ttu-id="54141-179">Note the column name need map to the schema being used in the query.</span><span class="sxs-lookup"><span data-stu-id="54141-179">Note the column name need map to the schema being used in the query.</span></span>

<span data-ttu-id="54141-180">**Sample query:**
`SELECT col_value FROM Actual.alm_asset` OR `SELECT col_display_value FROM Display.alm_asset`</span><span class="sxs-lookup"><span data-stu-id="54141-180">**Sample query:**
`SELECT col_value FROM Actual.alm_asset` OR `SELECT col_display_value FROM Display.alm_asset`</span></span>

<span data-ttu-id="54141-181">**Example:**</span><span class="sxs-lookup"><span data-stu-id="54141-181">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromServiceNow",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<ServiceNow input dataset name>",
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
                "type": "ServiceNowSource",
                "query": "SELECT * FROM Actual.alm_asset"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="54141-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="54141-182">Next steps</span></span>
<span data-ttu-id="54141-183">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="54141-183">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
