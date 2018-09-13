---
title: Copy data from Phoenix using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Phoenix to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 04/19/2017
ms.author: jingwang
ms.openlocfilehash: fc4eb2b717ea9f4c1b2813db7dcf02062948bae0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865790"
---
# <a name="copy-data-from-phoenix-using-azure-data-factory"></a><span data-ttu-id="f3e07-103">Copy data from Phoenix using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f3e07-103">Copy data from Phoenix using Azure Data Factory</span></span> 

<span data-ttu-id="f3e07-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Phoenix.</span><span class="sxs-lookup"><span data-stu-id="f3e07-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Phoenix.</span></span> <span data-ttu-id="f3e07-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="f3e07-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="f3e07-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="f3e07-106">Supported capabilities</span></span>

<span data-ttu-id="f3e07-107">You can copy data from Phoenix to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f3e07-107">You can copy data from Phoenix to any supported sink data store.</span></span> <span data-ttu-id="f3e07-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="f3e07-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="f3e07-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="f3e07-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f3e07-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="f3e07-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="f3e07-111">The following sections provide details about properties that are used to define Data Factory entities specific to Phoenix connector.</span><span class="sxs-lookup"><span data-stu-id="f3e07-111">The following sections provide details about properties that are used to define Data Factory entities specific to Phoenix connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f3e07-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f3e07-112">Linked service properties</span></span>

<span data-ttu-id="f3e07-113">The following properties are supported for Phoenix linked service:</span><span class="sxs-lookup"><span data-stu-id="f3e07-113">The following properties are supported for Phoenix linked service:</span></span>

| <span data-ttu-id="f3e07-114">Property</span><span class="sxs-lookup"><span data-stu-id="f3e07-114">Property</span></span> | <span data-ttu-id="f3e07-115">Description</span><span class="sxs-lookup"><span data-stu-id="f3e07-115">Description</span></span> | <span data-ttu-id="f3e07-116">Required</span><span class="sxs-lookup"><span data-stu-id="f3e07-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f3e07-117">type</span><span class="sxs-lookup"><span data-stu-id="f3e07-117">type</span></span> | <span data-ttu-id="f3e07-118">The type property must be set to: **Phoenix**</span><span class="sxs-lookup"><span data-stu-id="f3e07-118">The type property must be set to: **Phoenix**</span></span> | <span data-ttu-id="f3e07-119">Yes</span><span class="sxs-lookup"><span data-stu-id="f3e07-119">Yes</span></span> |
| <span data-ttu-id="f3e07-120">host</span><span class="sxs-lookup"><span data-stu-id="f3e07-120">host</span></span> | <span data-ttu-id="f3e07-121">The IP address or host name of the Phoenix server.</span><span class="sxs-lookup"><span data-stu-id="f3e07-121">The IP address or host name of the Phoenix server.</span></span> <span data-ttu-id="f3e07-122">(that is, 192.168.222.160)</span><span class="sxs-lookup"><span data-stu-id="f3e07-122">(that is, 192.168.222.160)</span></span>  | <span data-ttu-id="f3e07-123">Yes</span><span class="sxs-lookup"><span data-stu-id="f3e07-123">Yes</span></span> |
| <span data-ttu-id="f3e07-124">port</span><span class="sxs-lookup"><span data-stu-id="f3e07-124">port</span></span> | <span data-ttu-id="f3e07-125">The TCP port that the Phoenix server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="f3e07-125">The TCP port that the Phoenix server uses to listen for client connections.</span></span> <span data-ttu-id="f3e07-126">The default value is 8765.</span><span class="sxs-lookup"><span data-stu-id="f3e07-126">The default value is 8765.</span></span> <span data-ttu-id="f3e07-127">If you connect to Azure HDInsights, specify port as 443.</span><span class="sxs-lookup"><span data-stu-id="f3e07-127">If you connect to Azure HDInsights, specify port as 443.</span></span> | <span data-ttu-id="f3e07-128">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-128">No</span></span> |
| <span data-ttu-id="f3e07-129">httpPath</span><span class="sxs-lookup"><span data-stu-id="f3e07-129">httpPath</span></span> | <span data-ttu-id="f3e07-130">The partial URL corresponding to the Phoenix server.</span><span class="sxs-lookup"><span data-stu-id="f3e07-130">The partial URL corresponding to the Phoenix server.</span></span> <span data-ttu-id="f3e07-131">(that is, /gateway/sandbox/phoenix/version).</span><span class="sxs-lookup"><span data-stu-id="f3e07-131">(that is, /gateway/sandbox/phoenix/version).</span></span> <span data-ttu-id="f3e07-132">The default value is `hbasephoenix` if using WindowsAzureHDInsightService.</span><span class="sxs-lookup"><span data-stu-id="f3e07-132">The default value is `hbasephoenix` if using WindowsAzureHDInsightService.</span></span>  | <span data-ttu-id="f3e07-133">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-133">No</span></span> |
| <span data-ttu-id="f3e07-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f3e07-134">authenticationType</span></span> | <span data-ttu-id="f3e07-135">The authentication mechanism used to connect to the Phoenix server.</span><span class="sxs-lookup"><span data-stu-id="f3e07-135">The authentication mechanism used to connect to the Phoenix server.</span></span> <br/><span data-ttu-id="f3e07-136">Allowed values are: **Anonymous**, **UsernameAndPassword**, **WindowsAzureHDInsightService**</span><span class="sxs-lookup"><span data-stu-id="f3e07-136">Allowed values are: **Anonymous**, **UsernameAndPassword**, **WindowsAzureHDInsightService**</span></span> | <span data-ttu-id="f3e07-137">Yes</span><span class="sxs-lookup"><span data-stu-id="f3e07-137">Yes</span></span> |
| <span data-ttu-id="f3e07-138">username</span><span class="sxs-lookup"><span data-stu-id="f3e07-138">username</span></span> | <span data-ttu-id="f3e07-139">The user name used to connect to the Phoenix server.</span><span class="sxs-lookup"><span data-stu-id="f3e07-139">The user name used to connect to the Phoenix server.</span></span>  | <span data-ttu-id="f3e07-140">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-140">No</span></span> |
| <span data-ttu-id="f3e07-141">password</span><span class="sxs-lookup"><span data-stu-id="f3e07-141">password</span></span> | <span data-ttu-id="f3e07-142">The password corresponding to the user name.</span><span class="sxs-lookup"><span data-stu-id="f3e07-142">The password corresponding to the user name.</span></span> <span data-ttu-id="f3e07-143">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f3e07-143">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="f3e07-144">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-144">No</span></span> |
| <span data-ttu-id="f3e07-145">enableSsl</span><span class="sxs-lookup"><span data-stu-id="f3e07-145">enableSsl</span></span> | <span data-ttu-id="f3e07-146">Specifies whether the connections to the server are encrypted using SSL.</span><span class="sxs-lookup"><span data-stu-id="f3e07-146">Specifies whether the connections to the server are encrypted using SSL.</span></span> <span data-ttu-id="f3e07-147">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="f3e07-147">The default value is false.</span></span>  | <span data-ttu-id="f3e07-148">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-148">No</span></span> |
| <span data-ttu-id="f3e07-149">trustedCertPath</span><span class="sxs-lookup"><span data-stu-id="f3e07-149">trustedCertPath</span></span> | <span data-ttu-id="f3e07-150">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="f3e07-150">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span></span> <span data-ttu-id="f3e07-151">This property can only be set when using SSL on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="f3e07-151">This property can only be set when using SSL on self-hosted IR.</span></span> <span data-ttu-id="f3e07-152">The default value is the cacerts.pem file installed with the IR.</span><span class="sxs-lookup"><span data-stu-id="f3e07-152">The default value is the cacerts.pem file installed with the IR.</span></span>  | <span data-ttu-id="f3e07-153">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-153">No</span></span> |
| <span data-ttu-id="f3e07-154">useSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="f3e07-154">useSystemTrustStore</span></span> | <span data-ttu-id="f3e07-155">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span><span class="sxs-lookup"><span data-stu-id="f3e07-155">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span></span> <span data-ttu-id="f3e07-156">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="f3e07-156">The default value is false.</span></span>  | <span data-ttu-id="f3e07-157">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-157">No</span></span> |
| <span data-ttu-id="f3e07-158">allowHostNameCNMismatch</span><span class="sxs-lookup"><span data-stu-id="f3e07-158">allowHostNameCNMismatch</span></span> | <span data-ttu-id="f3e07-159">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="f3e07-159">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="f3e07-160">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="f3e07-160">The default value is false.</span></span>  | <span data-ttu-id="f3e07-161">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-161">No</span></span> |
| <span data-ttu-id="f3e07-162">allowSelfSignedServerCert</span><span class="sxs-lookup"><span data-stu-id="f3e07-162">allowSelfSignedServerCert</span></span> | <span data-ttu-id="f3e07-163">Specifies whether to allow self-signed certificates from the server.</span><span class="sxs-lookup"><span data-stu-id="f3e07-163">Specifies whether to allow self-signed certificates from the server.</span></span> <span data-ttu-id="f3e07-164">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="f3e07-164">The default value is false.</span></span>  | <span data-ttu-id="f3e07-165">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-165">No</span></span> |
| <span data-ttu-id="f3e07-166">connectVia</span><span class="sxs-lookup"><span data-stu-id="f3e07-166">connectVia</span></span> | <span data-ttu-id="f3e07-167">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="f3e07-167">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="f3e07-168">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="f3e07-168">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="f3e07-169">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="f3e07-169">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="f3e07-170">No</span><span class="sxs-lookup"><span data-stu-id="f3e07-170">No</span></span> |

<span data-ttu-id="f3e07-171">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f3e07-171">**Example:**</span></span>

```json
{
    "name": "PhoenixLinkedService",
    "properties": {
        "type": "Phoenix",
        "typeProperties": {
            "host" : "<cluster>.azurehdinsight.net",
            "port" : "443",
            "httpPath" : "hbasephoenix",
            "authenticationType" : "WindowsAzureHDInsightService",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f3e07-172">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f3e07-172">Dataset properties</span></span>

<span data-ttu-id="f3e07-173">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="f3e07-173">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="f3e07-174">This section provides a list of properties supported by Phoenix dataset.</span><span class="sxs-lookup"><span data-stu-id="f3e07-174">This section provides a list of properties supported by Phoenix dataset.</span></span>

<span data-ttu-id="f3e07-175">To copy data from Phoenix, set the type property of the dataset to **PhoenixObject**.</span><span class="sxs-lookup"><span data-stu-id="f3e07-175">To copy data from Phoenix, set the type property of the dataset to **PhoenixObject**.</span></span> <span data-ttu-id="f3e07-176">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="f3e07-176">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="f3e07-177">**Example**</span><span class="sxs-lookup"><span data-stu-id="f3e07-177">**Example**</span></span>

```json
{
    "name": "PhoenixDataset",
    "properties": {
        "type": "PhoenixObject",
        "linkedServiceName": {
            "referenceName": "<Phoenix linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="f3e07-178">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f3e07-178">Copy activity properties</span></span>

<span data-ttu-id="f3e07-179">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="f3e07-179">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="f3e07-180">This section provides a list of properties supported by Phoenix source.</span><span class="sxs-lookup"><span data-stu-id="f3e07-180">This section provides a list of properties supported by Phoenix source.</span></span>

### <a name="phoenixsource-as-source"></a><span data-ttu-id="f3e07-181">PhoenixSource as source</span><span class="sxs-lookup"><span data-stu-id="f3e07-181">PhoenixSource as source</span></span>

<span data-ttu-id="f3e07-182">To copy data from Phoenix, set the source type in the copy activity to **PhoenixSource**.</span><span class="sxs-lookup"><span data-stu-id="f3e07-182">To copy data from Phoenix, set the source type in the copy activity to **PhoenixSource**.</span></span> <span data-ttu-id="f3e07-183">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="f3e07-183">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="f3e07-184">Property</span><span class="sxs-lookup"><span data-stu-id="f3e07-184">Property</span></span> | <span data-ttu-id="f3e07-185">Description</span><span class="sxs-lookup"><span data-stu-id="f3e07-185">Description</span></span> | <span data-ttu-id="f3e07-186">Required</span><span class="sxs-lookup"><span data-stu-id="f3e07-186">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f3e07-187">type</span><span class="sxs-lookup"><span data-stu-id="f3e07-187">type</span></span> | <span data-ttu-id="f3e07-188">The type property of the copy activity source must be set to: **PhoenixSource**</span><span class="sxs-lookup"><span data-stu-id="f3e07-188">The type property of the copy activity source must be set to: **PhoenixSource**</span></span> | <span data-ttu-id="f3e07-189">Yes</span><span class="sxs-lookup"><span data-stu-id="f3e07-189">Yes</span></span> |
| <span data-ttu-id="f3e07-190">query</span><span class="sxs-lookup"><span data-stu-id="f3e07-190">query</span></span> | <span data-ttu-id="f3e07-191">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="f3e07-191">Use the custom SQL query to read data.</span></span> <span data-ttu-id="f3e07-192">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="f3e07-192">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="f3e07-193">Yes</span><span class="sxs-lookup"><span data-stu-id="f3e07-193">Yes</span></span> |

<span data-ttu-id="f3e07-194">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f3e07-194">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromPhoenix",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Phoenix input dataset name>",
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
                "type": "PhoenixSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="f3e07-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3e07-195">Next steps</span></span>
<span data-ttu-id="f3e07-196">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f3e07-196">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
