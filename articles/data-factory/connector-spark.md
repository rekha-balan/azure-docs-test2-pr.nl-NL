---
title: Copy data from Spark using Azure Data Factory  | Microsoft Docs
description: Learn how to copy data from Spark to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: a9b4de73c04d7c7c753f007c02c775366b882e81
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968919"
---
# <a name="copy-data-from-spark-using-azure-data-factory"></a><span data-ttu-id="9420b-103">Copy data from Spark using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9420b-103">Copy data from Spark using Azure Data Factory</span></span> 

<span data-ttu-id="9420b-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Spark.</span><span class="sxs-lookup"><span data-stu-id="9420b-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Spark.</span></span> <span data-ttu-id="9420b-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="9420b-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="9420b-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="9420b-106">Supported capabilities</span></span>

<span data-ttu-id="9420b-107">You can copy data from Spark to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="9420b-107">You can copy data from Spark to any supported sink data store.</span></span> <span data-ttu-id="9420b-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="9420b-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="9420b-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="9420b-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9420b-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="9420b-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="9420b-111">The following sections provide details about properties that are used to define Data Factory entities specific to Spark connector.</span><span class="sxs-lookup"><span data-stu-id="9420b-111">The following sections provide details about properties that are used to define Data Factory entities specific to Spark connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9420b-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="9420b-112">Linked service properties</span></span>

<span data-ttu-id="9420b-113">The following properties are supported for Spark linked service:</span><span class="sxs-lookup"><span data-stu-id="9420b-113">The following properties are supported for Spark linked service:</span></span>

| <span data-ttu-id="9420b-114">Property</span><span class="sxs-lookup"><span data-stu-id="9420b-114">Property</span></span> | <span data-ttu-id="9420b-115">Description</span><span class="sxs-lookup"><span data-stu-id="9420b-115">Description</span></span> | <span data-ttu-id="9420b-116">Required</span><span class="sxs-lookup"><span data-stu-id="9420b-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9420b-117">type</span><span class="sxs-lookup"><span data-stu-id="9420b-117">type</span></span> | <span data-ttu-id="9420b-118">The type property must be set to: **Spark**</span><span class="sxs-lookup"><span data-stu-id="9420b-118">The type property must be set to: **Spark**</span></span> | <span data-ttu-id="9420b-119">Yes</span><span class="sxs-lookup"><span data-stu-id="9420b-119">Yes</span></span> |
| <span data-ttu-id="9420b-120">host</span><span class="sxs-lookup"><span data-stu-id="9420b-120">host</span></span> | <span data-ttu-id="9420b-121">IP address or host name of the Spark server</span><span class="sxs-lookup"><span data-stu-id="9420b-121">IP address or host name of the Spark server</span></span>  | <span data-ttu-id="9420b-122">Yes</span><span class="sxs-lookup"><span data-stu-id="9420b-122">Yes</span></span> |
| <span data-ttu-id="9420b-123">port</span><span class="sxs-lookup"><span data-stu-id="9420b-123">port</span></span> | <span data-ttu-id="9420b-124">The TCP port that the Spark server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="9420b-124">The TCP port that the Spark server uses to listen for client connections.</span></span> <span data-ttu-id="9420b-125">If you connect to Azure HDInsights, specify port as 443.</span><span class="sxs-lookup"><span data-stu-id="9420b-125">If you connect to Azure HDInsights, specify port as 443.</span></span> | <span data-ttu-id="9420b-126">Yes</span><span class="sxs-lookup"><span data-stu-id="9420b-126">Yes</span></span> |
| <span data-ttu-id="9420b-127">serverType</span><span class="sxs-lookup"><span data-stu-id="9420b-127">serverType</span></span> | <span data-ttu-id="9420b-128">The type of Spark server.</span><span class="sxs-lookup"><span data-stu-id="9420b-128">The type of Spark server.</span></span> <br/><span data-ttu-id="9420b-129">Allowed values are: **SharkServer**, **SharkServer2**, **SparkThriftServer**</span><span class="sxs-lookup"><span data-stu-id="9420b-129">Allowed values are: **SharkServer**, **SharkServer2**, **SparkThriftServer**</span></span> | <span data-ttu-id="9420b-130">No</span><span class="sxs-lookup"><span data-stu-id="9420b-130">No</span></span> |
| <span data-ttu-id="9420b-131">thriftTransportProtocol</span><span class="sxs-lookup"><span data-stu-id="9420b-131">thriftTransportProtocol</span></span> | <span data-ttu-id="9420b-132">The transport protocol to use in the Thrift layer.</span><span class="sxs-lookup"><span data-stu-id="9420b-132">The transport protocol to use in the Thrift layer.</span></span> <br/><span data-ttu-id="9420b-133">Allowed values are: **Binary**, **SASL**, **HTTP**</span><span class="sxs-lookup"><span data-stu-id="9420b-133">Allowed values are: **Binary**, **SASL**, **HTTP**</span></span> | <span data-ttu-id="9420b-134">No</span><span class="sxs-lookup"><span data-stu-id="9420b-134">No</span></span> |
| <span data-ttu-id="9420b-135">authenticationType</span><span class="sxs-lookup"><span data-stu-id="9420b-135">authenticationType</span></span> | <span data-ttu-id="9420b-136">The authentication method used to access the Spark server.</span><span class="sxs-lookup"><span data-stu-id="9420b-136">The authentication method used to access the Spark server.</span></span> <br/><span data-ttu-id="9420b-137">Allowed values are: **Anonymous**, **Username**, **UsernameAndPassword**, **WindowsAzureHDInsightService**</span><span class="sxs-lookup"><span data-stu-id="9420b-137">Allowed values are: **Anonymous**, **Username**, **UsernameAndPassword**, **WindowsAzureHDInsightService**</span></span> | <span data-ttu-id="9420b-138">Yes</span><span class="sxs-lookup"><span data-stu-id="9420b-138">Yes</span></span> |
| <span data-ttu-id="9420b-139">username</span><span class="sxs-lookup"><span data-stu-id="9420b-139">username</span></span> | <span data-ttu-id="9420b-140">The user name that you use to access Spark Server.</span><span class="sxs-lookup"><span data-stu-id="9420b-140">The user name that you use to access Spark Server.</span></span>  | <span data-ttu-id="9420b-141">No</span><span class="sxs-lookup"><span data-stu-id="9420b-141">No</span></span> |
| <span data-ttu-id="9420b-142">password</span><span class="sxs-lookup"><span data-stu-id="9420b-142">password</span></span> | <span data-ttu-id="9420b-143">The password corresponding to the user.</span><span class="sxs-lookup"><span data-stu-id="9420b-143">The password corresponding to the user.</span></span> <span data-ttu-id="9420b-144">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="9420b-144">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="9420b-145">No</span><span class="sxs-lookup"><span data-stu-id="9420b-145">No</span></span> |
| <span data-ttu-id="9420b-146">httpPath</span><span class="sxs-lookup"><span data-stu-id="9420b-146">httpPath</span></span> | <span data-ttu-id="9420b-147">The partial URL corresponding to the Spark server.</span><span class="sxs-lookup"><span data-stu-id="9420b-147">The partial URL corresponding to the Spark server.</span></span>  | <span data-ttu-id="9420b-148">No</span><span class="sxs-lookup"><span data-stu-id="9420b-148">No</span></span> |
| <span data-ttu-id="9420b-149">enableSsl</span><span class="sxs-lookup"><span data-stu-id="9420b-149">enableSsl</span></span> | <span data-ttu-id="9420b-150">Specifies whether the connections to the server are encrypted using SSL.</span><span class="sxs-lookup"><span data-stu-id="9420b-150">Specifies whether the connections to the server are encrypted using SSL.</span></span> <span data-ttu-id="9420b-151">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="9420b-151">The default value is false.</span></span>  | <span data-ttu-id="9420b-152">No</span><span class="sxs-lookup"><span data-stu-id="9420b-152">No</span></span> |
| <span data-ttu-id="9420b-153">trustedCertPath</span><span class="sxs-lookup"><span data-stu-id="9420b-153">trustedCertPath</span></span> | <span data-ttu-id="9420b-154">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="9420b-154">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span></span> <span data-ttu-id="9420b-155">This property can only be set when using SSL on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="9420b-155">This property can only be set when using SSL on self-hosted IR.</span></span> <span data-ttu-id="9420b-156">The default value is the cacerts.pem file installed with the IR.</span><span class="sxs-lookup"><span data-stu-id="9420b-156">The default value is the cacerts.pem file installed with the IR.</span></span>  | <span data-ttu-id="9420b-157">No</span><span class="sxs-lookup"><span data-stu-id="9420b-157">No</span></span> |
| <span data-ttu-id="9420b-158">useSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="9420b-158">useSystemTrustStore</span></span> | <span data-ttu-id="9420b-159">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span><span class="sxs-lookup"><span data-stu-id="9420b-159">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span></span> <span data-ttu-id="9420b-160">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="9420b-160">The default value is false.</span></span>  | <span data-ttu-id="9420b-161">No</span><span class="sxs-lookup"><span data-stu-id="9420b-161">No</span></span> |
| <span data-ttu-id="9420b-162">allowHostNameCNMismatch</span><span class="sxs-lookup"><span data-stu-id="9420b-162">allowHostNameCNMismatch</span></span> | <span data-ttu-id="9420b-163">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="9420b-163">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="9420b-164">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="9420b-164">The default value is false.</span></span>  | <span data-ttu-id="9420b-165">No</span><span class="sxs-lookup"><span data-stu-id="9420b-165">No</span></span> |
| <span data-ttu-id="9420b-166">allowSelfSignedServerCert</span><span class="sxs-lookup"><span data-stu-id="9420b-166">allowSelfSignedServerCert</span></span> | <span data-ttu-id="9420b-167">Specifies whether to allow self-signed certificates from the server.</span><span class="sxs-lookup"><span data-stu-id="9420b-167">Specifies whether to allow self-signed certificates from the server.</span></span> <span data-ttu-id="9420b-168">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="9420b-168">The default value is false.</span></span>  | <span data-ttu-id="9420b-169">No</span><span class="sxs-lookup"><span data-stu-id="9420b-169">No</span></span> |
| <span data-ttu-id="9420b-170">connectVia</span><span class="sxs-lookup"><span data-stu-id="9420b-170">connectVia</span></span> | <span data-ttu-id="9420b-171">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="9420b-171">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="9420b-172">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="9420b-172">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="9420b-173">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="9420b-173">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="9420b-174">No</span><span class="sxs-lookup"><span data-stu-id="9420b-174">No</span></span> |

<span data-ttu-id="9420b-175">**Example:**</span><span class="sxs-lookup"><span data-stu-id="9420b-175">**Example:**</span></span>

```json
{
    "name": "SparkLinkedService",
    "properties": {
        "type": "Spark",
        "typeProperties": {
            "host" : "<cluster>.azurehdinsight.net",
            "port" : "<port>",
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

## <a name="dataset-properties"></a><span data-ttu-id="9420b-176">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="9420b-176">Dataset properties</span></span>

<span data-ttu-id="9420b-177">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="9420b-177">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="9420b-178">This section provides a list of properties supported by Spark dataset.</span><span class="sxs-lookup"><span data-stu-id="9420b-178">This section provides a list of properties supported by Spark dataset.</span></span>

<span data-ttu-id="9420b-179">To copy data from Spark, set the type property of the dataset to **SparkObject**.</span><span class="sxs-lookup"><span data-stu-id="9420b-179">To copy data from Spark, set the type property of the dataset to **SparkObject**.</span></span> <span data-ttu-id="9420b-180">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="9420b-180">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="9420b-181">**Example**</span><span class="sxs-lookup"><span data-stu-id="9420b-181">**Example**</span></span>

```json
{
    "name": "SparkDataset",
    "properties": {
        "type": "SparkObject",
        "linkedServiceName": {
            "referenceName": "<Spark linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="9420b-182">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="9420b-182">Copy activity properties</span></span>

<span data-ttu-id="9420b-183">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="9420b-183">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="9420b-184">This section provides a list of properties supported by Spark source.</span><span class="sxs-lookup"><span data-stu-id="9420b-184">This section provides a list of properties supported by Spark source.</span></span>

### <a name="sparksource-as-source"></a><span data-ttu-id="9420b-185">SparkSource as source</span><span class="sxs-lookup"><span data-stu-id="9420b-185">SparkSource as source</span></span>

<span data-ttu-id="9420b-186">To copy data from Spark, set the source type in the copy activity to **SparkSource**.</span><span class="sxs-lookup"><span data-stu-id="9420b-186">To copy data from Spark, set the source type in the copy activity to **SparkSource**.</span></span> <span data-ttu-id="9420b-187">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="9420b-187">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="9420b-188">Property</span><span class="sxs-lookup"><span data-stu-id="9420b-188">Property</span></span> | <span data-ttu-id="9420b-189">Description</span><span class="sxs-lookup"><span data-stu-id="9420b-189">Description</span></span> | <span data-ttu-id="9420b-190">Required</span><span class="sxs-lookup"><span data-stu-id="9420b-190">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9420b-191">type</span><span class="sxs-lookup"><span data-stu-id="9420b-191">type</span></span> | <span data-ttu-id="9420b-192">The type property of the copy activity source must be set to: **SparkSource**</span><span class="sxs-lookup"><span data-stu-id="9420b-192">The type property of the copy activity source must be set to: **SparkSource**</span></span> | <span data-ttu-id="9420b-193">Yes</span><span class="sxs-lookup"><span data-stu-id="9420b-193">Yes</span></span> |
| <span data-ttu-id="9420b-194">query</span><span class="sxs-lookup"><span data-stu-id="9420b-194">query</span></span> | <span data-ttu-id="9420b-195">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="9420b-195">Use the custom SQL query to read data.</span></span> <span data-ttu-id="9420b-196">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="9420b-196">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="9420b-197">Yes</span><span class="sxs-lookup"><span data-stu-id="9420b-197">Yes</span></span> |

<span data-ttu-id="9420b-198">**Example:**</span><span class="sxs-lookup"><span data-stu-id="9420b-198">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSpark",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Spark input dataset name>",
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
                "type": "SparkSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="9420b-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="9420b-199">Next steps</span></span>
<span data-ttu-id="9420b-200">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9420b-200">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
