---
title: Copy data from HBase using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from HBase to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 04/19/2018
ms.author: jingwang
ms.openlocfilehash: f47e85b47f262e30e9160f11604220aa8055be5d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865634"
---
# <a name="copy-data-from-hbase-using-azure-data-factory"></a><span data-ttu-id="01fb1-103">Copy data from HBase using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="01fb1-103">Copy data from HBase using Azure Data Factory</span></span> 

<span data-ttu-id="01fb1-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from HBase.</span><span class="sxs-lookup"><span data-stu-id="01fb1-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from HBase.</span></span> <span data-ttu-id="01fb1-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="01fb1-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="01fb1-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="01fb1-106">Supported capabilities</span></span>

<span data-ttu-id="01fb1-107">You can copy data from HBase to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="01fb1-107">You can copy data from HBase to any supported sink data store.</span></span> <span data-ttu-id="01fb1-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="01fb1-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="01fb1-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="01fb1-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="01fb1-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="01fb1-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="01fb1-111">The following sections provide details about properties that are used to define Data Factory entities specific to HBase connector.</span><span class="sxs-lookup"><span data-stu-id="01fb1-111">The following sections provide details about properties that are used to define Data Factory entities specific to HBase connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="01fb1-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="01fb1-112">Linked service properties</span></span>

<span data-ttu-id="01fb1-113">The following properties are supported for HBase linked service:</span><span class="sxs-lookup"><span data-stu-id="01fb1-113">The following properties are supported for HBase linked service:</span></span>

| <span data-ttu-id="01fb1-114">Property</span><span class="sxs-lookup"><span data-stu-id="01fb1-114">Property</span></span> | <span data-ttu-id="01fb1-115">Description</span><span class="sxs-lookup"><span data-stu-id="01fb1-115">Description</span></span> | <span data-ttu-id="01fb1-116">Required</span><span class="sxs-lookup"><span data-stu-id="01fb1-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="01fb1-117">type</span><span class="sxs-lookup"><span data-stu-id="01fb1-117">type</span></span> | <span data-ttu-id="01fb1-118">The type property must be set to: **HBase**</span><span class="sxs-lookup"><span data-stu-id="01fb1-118">The type property must be set to: **HBase**</span></span> | <span data-ttu-id="01fb1-119">Yes</span><span class="sxs-lookup"><span data-stu-id="01fb1-119">Yes</span></span> |
| <span data-ttu-id="01fb1-120">host</span><span class="sxs-lookup"><span data-stu-id="01fb1-120">host</span></span> | <span data-ttu-id="01fb1-121">The IP address or host name of the HBase server.</span><span class="sxs-lookup"><span data-stu-id="01fb1-121">The IP address or host name of the HBase server.</span></span> <span data-ttu-id="01fb1-122">(i.e.  `[clustername].azurehdinsight.net`， \`192.168.222.160·)</span><span class="sxs-lookup"><span data-stu-id="01fb1-122">(i.e.  `[clustername].azurehdinsight.net`， \`192.168.222.160·)</span></span>  | <span data-ttu-id="01fb1-123">Yes</span><span class="sxs-lookup"><span data-stu-id="01fb1-123">Yes</span></span> |
| <span data-ttu-id="01fb1-124">port</span><span class="sxs-lookup"><span data-stu-id="01fb1-124">port</span></span> | <span data-ttu-id="01fb1-125">The TCP port that the HBase instance uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="01fb1-125">The TCP port that the HBase instance uses to listen for client connections.</span></span> <span data-ttu-id="01fb1-126">The default value is 9090.</span><span class="sxs-lookup"><span data-stu-id="01fb1-126">The default value is 9090.</span></span> <span data-ttu-id="01fb1-127">If you connect to Azure HDInsights, specify port as 443.</span><span class="sxs-lookup"><span data-stu-id="01fb1-127">If you connect to Azure HDInsights, specify port as 443.</span></span> | <span data-ttu-id="01fb1-128">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-128">No</span></span> |
| <span data-ttu-id="01fb1-129">httpPath</span><span class="sxs-lookup"><span data-stu-id="01fb1-129">httpPath</span></span> | <span data-ttu-id="01fb1-130">The partial URL corresponding to the HBase server.</span><span class="sxs-lookup"><span data-stu-id="01fb1-130">The partial URL corresponding to the HBase server.</span></span> <span data-ttu-id="01fb1-131">(i.e. `/hbaserest0`)</span><span class="sxs-lookup"><span data-stu-id="01fb1-131">(i.e. `/hbaserest0`)</span></span>  | <span data-ttu-id="01fb1-132">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-132">No</span></span> |
| <span data-ttu-id="01fb1-133">authenticationType</span><span class="sxs-lookup"><span data-stu-id="01fb1-133">authenticationType</span></span> | <span data-ttu-id="01fb1-134">The authentication mechanism to use to connect to the HBase server.</span><span class="sxs-lookup"><span data-stu-id="01fb1-134">The authentication mechanism to use to connect to the HBase server.</span></span> <br/><span data-ttu-id="01fb1-135">Allowed values are: **Anonymous**, **Basic**</span><span class="sxs-lookup"><span data-stu-id="01fb1-135">Allowed values are: **Anonymous**, **Basic**</span></span> | <span data-ttu-id="01fb1-136">Yes</span><span class="sxs-lookup"><span data-stu-id="01fb1-136">Yes</span></span> |
| <span data-ttu-id="01fb1-137">username</span><span class="sxs-lookup"><span data-stu-id="01fb1-137">username</span></span> | <span data-ttu-id="01fb1-138">The user name used to connect to the HBase instance.</span><span class="sxs-lookup"><span data-stu-id="01fb1-138">The user name used to connect to the HBase instance.</span></span>  | <span data-ttu-id="01fb1-139">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-139">No</span></span> |
| <span data-ttu-id="01fb1-140">password</span><span class="sxs-lookup"><span data-stu-id="01fb1-140">password</span></span> | <span data-ttu-id="01fb1-141">The password corresponding to the user name.</span><span class="sxs-lookup"><span data-stu-id="01fb1-141">The password corresponding to the user name.</span></span> <span data-ttu-id="01fb1-142">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="01fb1-142">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="01fb1-143">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-143">No</span></span> |
| <span data-ttu-id="01fb1-144">enableSsl</span><span class="sxs-lookup"><span data-stu-id="01fb1-144">enableSsl</span></span> | <span data-ttu-id="01fb1-145">Specifies whether the connections to the server are encrypted using SSL.</span><span class="sxs-lookup"><span data-stu-id="01fb1-145">Specifies whether the connections to the server are encrypted using SSL.</span></span> <span data-ttu-id="01fb1-146">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="01fb1-146">The default value is false.</span></span>  | <span data-ttu-id="01fb1-147">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-147">No</span></span> |
| <span data-ttu-id="01fb1-148">trustedCertPath</span><span class="sxs-lookup"><span data-stu-id="01fb1-148">trustedCertPath</span></span> | <span data-ttu-id="01fb1-149">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="01fb1-149">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span></span> <span data-ttu-id="01fb1-150">This property can only be set when using SSL on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="01fb1-150">This property can only be set when using SSL on self-hosted IR.</span></span> <span data-ttu-id="01fb1-151">The default value is the cacerts.pem file installed with the IR.</span><span class="sxs-lookup"><span data-stu-id="01fb1-151">The default value is the cacerts.pem file installed with the IR.</span></span>  | <span data-ttu-id="01fb1-152">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-152">No</span></span> |
| <span data-ttu-id="01fb1-153">allowHostNameCNMismatch</span><span class="sxs-lookup"><span data-stu-id="01fb1-153">allowHostNameCNMismatch</span></span> | <span data-ttu-id="01fb1-154">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="01fb1-154">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="01fb1-155">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="01fb1-155">The default value is false.</span></span>  | <span data-ttu-id="01fb1-156">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-156">No</span></span> |
| <span data-ttu-id="01fb1-157">allowSelfSignedServerCert</span><span class="sxs-lookup"><span data-stu-id="01fb1-157">allowSelfSignedServerCert</span></span> | <span data-ttu-id="01fb1-158">Specifies whether to allow self-signed certificates from the server.</span><span class="sxs-lookup"><span data-stu-id="01fb1-158">Specifies whether to allow self-signed certificates from the server.</span></span> <span data-ttu-id="01fb1-159">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="01fb1-159">The default value is false.</span></span>  | <span data-ttu-id="01fb1-160">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-160">No</span></span> |
| <span data-ttu-id="01fb1-161">connectVia</span><span class="sxs-lookup"><span data-stu-id="01fb1-161">connectVia</span></span> | <span data-ttu-id="01fb1-162">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="01fb1-162">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="01fb1-163">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="01fb1-163">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="01fb1-164">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="01fb1-164">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="01fb1-165">No</span><span class="sxs-lookup"><span data-stu-id="01fb1-165">No</span></span> |

>[!NOTE]
><span data-ttu-id="01fb1-166">If your cluster doesn't support sticky session like HDInsight, explicitly add node index at the end of the http path setting, e.g. specify `/hbaserest0` instead of `/hbaserest`.</span><span class="sxs-lookup"><span data-stu-id="01fb1-166">If your cluster doesn't support sticky session like HDInsight, explicitly add node index at the end of the http path setting, e.g. specify `/hbaserest0` instead of `/hbaserest`.</span></span>

<span data-ttu-id="01fb1-167">**Example for HDInsights HBase:**</span><span class="sxs-lookup"><span data-stu-id="01fb1-167">**Example for HDInsights HBase:**</span></span>

```json
{
    "name": "HBaseLinkedService",
    "properties": {
        "type": "HBase",
        "typeProperties": {
            "host" : "<cluster name>.azurehdinsight.net",
            "port" : "443",
            "httpPath" : "/hbaserest0",
            "authenticationType" : "Basic",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            },
            "enableSsl" : true
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="01fb1-168">**Example for generic HBase:**</span><span class="sxs-lookup"><span data-stu-id="01fb1-168">**Example for generic HBase:**</span></span>

```json
{
    "name": "HBaseLinkedService",
    "properties": {
        "type": "HBase",
        "typeProperties": {
            "host" : "<host e.g. 192.168.222.160>",
            "port" : "<port>",
            "httpPath" : "<e.g. /gateway/sandbox/hbase/version>",
            "authenticationType" : "Basic",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            },
            "enableSsl" : true,
            "trustedCertPath" : "<trustedCertPath>",
            "allowHostNameCNMismatch" : true,
            "allowSelfSignedServerCert" : true
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="01fb1-169">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="01fb1-169">Dataset properties</span></span>

<span data-ttu-id="01fb1-170">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="01fb1-170">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="01fb1-171">This section provides a list of properties supported by HBase dataset.</span><span class="sxs-lookup"><span data-stu-id="01fb1-171">This section provides a list of properties supported by HBase dataset.</span></span>

<span data-ttu-id="01fb1-172">To copy data from HBase, set the type property of the dataset to **HBaseObject**.</span><span class="sxs-lookup"><span data-stu-id="01fb1-172">To copy data from HBase, set the type property of the dataset to **HBaseObject**.</span></span> <span data-ttu-id="01fb1-173">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="01fb1-173">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="01fb1-174">**Example**</span><span class="sxs-lookup"><span data-stu-id="01fb1-174">**Example**</span></span>

```json
{
    "name": "HBaseDataset",
    "properties": {
        "type": "HBaseObject",
        "linkedServiceName": {
            "referenceName": "<HBase linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="01fb1-175">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="01fb1-175">Copy activity properties</span></span>

<span data-ttu-id="01fb1-176">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="01fb1-176">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="01fb1-177">This section provides a list of properties supported by HBase source.</span><span class="sxs-lookup"><span data-stu-id="01fb1-177">This section provides a list of properties supported by HBase source.</span></span>

### <a name="hbasesource-as-source"></a><span data-ttu-id="01fb1-178">HBaseSource as source</span><span class="sxs-lookup"><span data-stu-id="01fb1-178">HBaseSource as source</span></span>

<span data-ttu-id="01fb1-179">To copy data from HBase, set the source type in the copy activity to **HBaseSource**.</span><span class="sxs-lookup"><span data-stu-id="01fb1-179">To copy data from HBase, set the source type in the copy activity to **HBaseSource**.</span></span> <span data-ttu-id="01fb1-180">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="01fb1-180">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="01fb1-181">Property</span><span class="sxs-lookup"><span data-stu-id="01fb1-181">Property</span></span> | <span data-ttu-id="01fb1-182">Description</span><span class="sxs-lookup"><span data-stu-id="01fb1-182">Description</span></span> | <span data-ttu-id="01fb1-183">Required</span><span class="sxs-lookup"><span data-stu-id="01fb1-183">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="01fb1-184">type</span><span class="sxs-lookup"><span data-stu-id="01fb1-184">type</span></span> | <span data-ttu-id="01fb1-185">The type property of the copy activity source must be set to: **HBaseSource**</span><span class="sxs-lookup"><span data-stu-id="01fb1-185">The type property of the copy activity source must be set to: **HBaseSource**</span></span> | <span data-ttu-id="01fb1-186">Yes</span><span class="sxs-lookup"><span data-stu-id="01fb1-186">Yes</span></span> |
| <span data-ttu-id="01fb1-187">query</span><span class="sxs-lookup"><span data-stu-id="01fb1-187">query</span></span> | <span data-ttu-id="01fb1-188">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="01fb1-188">Use the custom SQL query to read data.</span></span> <span data-ttu-id="01fb1-189">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="01fb1-189">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="01fb1-190">Yes</span><span class="sxs-lookup"><span data-stu-id="01fb1-190">Yes</span></span> |

<span data-ttu-id="01fb1-191">**Example:**</span><span class="sxs-lookup"><span data-stu-id="01fb1-191">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromHBase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<HBase input dataset name>",
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
                "type": "HBaseSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="01fb1-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="01fb1-192">Next steps</span></span>
<span data-ttu-id="01fb1-193">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="01fb1-193">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
