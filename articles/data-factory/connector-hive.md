---
title: Copy data from Hive using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Hive to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 379cc5412d317680afa9b03f0eea60c7f1a3b60d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871245"
---
# <a name="copy-data-from-hive-using-azure-data-factory"></a><span data-ttu-id="d7069-103">Copy data from Hive using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d7069-103">Copy data from Hive using Azure Data Factory</span></span> 

<span data-ttu-id="d7069-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Hive.</span><span class="sxs-lookup"><span data-stu-id="d7069-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Hive.</span></span> <span data-ttu-id="d7069-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="d7069-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="d7069-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="d7069-106">Supported capabilities</span></span>

<span data-ttu-id="d7069-107">You can copy data from Hive to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="d7069-107">You can copy data from Hive to any supported sink data store.</span></span> <span data-ttu-id="d7069-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="d7069-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="d7069-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="d7069-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d7069-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="d7069-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="d7069-111">The following sections provide details about properties that are used to define Data Factory entities specific to Hive connector.</span><span class="sxs-lookup"><span data-stu-id="d7069-111">The following sections provide details about properties that are used to define Data Factory entities specific to Hive connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d7069-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="d7069-112">Linked service properties</span></span>

<span data-ttu-id="d7069-113">The following properties are supported for Hive linked service:</span><span class="sxs-lookup"><span data-stu-id="d7069-113">The following properties are supported for Hive linked service:</span></span>

| <span data-ttu-id="d7069-114">Property</span><span class="sxs-lookup"><span data-stu-id="d7069-114">Property</span></span> | <span data-ttu-id="d7069-115">Description</span><span class="sxs-lookup"><span data-stu-id="d7069-115">Description</span></span> | <span data-ttu-id="d7069-116">Required</span><span class="sxs-lookup"><span data-stu-id="d7069-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d7069-117">type</span><span class="sxs-lookup"><span data-stu-id="d7069-117">type</span></span> | <span data-ttu-id="d7069-118">The type property must be set to: **Hive**</span><span class="sxs-lookup"><span data-stu-id="d7069-118">The type property must be set to: **Hive**</span></span> | <span data-ttu-id="d7069-119">Yes</span><span class="sxs-lookup"><span data-stu-id="d7069-119">Yes</span></span> |
| <span data-ttu-id="d7069-120">host</span><span class="sxs-lookup"><span data-stu-id="d7069-120">host</span></span> | <span data-ttu-id="d7069-121">IP address or host name of the Hive server, separated by ';' for multiple hosts (only when serviceDiscoveryMode is enable).</span><span class="sxs-lookup"><span data-stu-id="d7069-121">IP address or host name of the Hive server, separated by ';' for multiple hosts (only when serviceDiscoveryMode is enable).</span></span>  | <span data-ttu-id="d7069-122">Yes</span><span class="sxs-lookup"><span data-stu-id="d7069-122">Yes</span></span> |
| <span data-ttu-id="d7069-123">port</span><span class="sxs-lookup"><span data-stu-id="d7069-123">port</span></span> | <span data-ttu-id="d7069-124">The TCP port that the Hive server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="d7069-124">The TCP port that the Hive server uses to listen for client connections.</span></span> <span data-ttu-id="d7069-125">If you connect to Azure HDInsights, specify port as 443.</span><span class="sxs-lookup"><span data-stu-id="d7069-125">If you connect to Azure HDInsights, specify port as 443.</span></span> | <span data-ttu-id="d7069-126">Yes</span><span class="sxs-lookup"><span data-stu-id="d7069-126">Yes</span></span> |
| <span data-ttu-id="d7069-127">serverType</span><span class="sxs-lookup"><span data-stu-id="d7069-127">serverType</span></span> | <span data-ttu-id="d7069-128">The type of Hive server.</span><span class="sxs-lookup"><span data-stu-id="d7069-128">The type of Hive server.</span></span> <br/><span data-ttu-id="d7069-129">Allowed values are: **HiveServer1**, **HiveServer2**, **HiveThriftServer**</span><span class="sxs-lookup"><span data-stu-id="d7069-129">Allowed values are: **HiveServer1**, **HiveServer2**, **HiveThriftServer**</span></span> | <span data-ttu-id="d7069-130">No</span><span class="sxs-lookup"><span data-stu-id="d7069-130">No</span></span> |
| <span data-ttu-id="d7069-131">thriftTransportProtocol</span><span class="sxs-lookup"><span data-stu-id="d7069-131">thriftTransportProtocol</span></span> | <span data-ttu-id="d7069-132">The transport protocol to use in the Thrift layer.</span><span class="sxs-lookup"><span data-stu-id="d7069-132">The transport protocol to use in the Thrift layer.</span></span> <br/><span data-ttu-id="d7069-133">Allowed values are: **Binary**, **SASL**, **HTTP**</span><span class="sxs-lookup"><span data-stu-id="d7069-133">Allowed values are: **Binary**, **SASL**, **HTTP**</span></span> | <span data-ttu-id="d7069-134">No</span><span class="sxs-lookup"><span data-stu-id="d7069-134">No</span></span> |
| <span data-ttu-id="d7069-135">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d7069-135">authenticationType</span></span> | <span data-ttu-id="d7069-136">The authentication method used to access the Hive server.</span><span class="sxs-lookup"><span data-stu-id="d7069-136">The authentication method used to access the Hive server.</span></span> <br/><span data-ttu-id="d7069-137">Allowed values are: **Anonymous**, **Username**, **UsernameAndPassword**, **WindowsAzureHDInsightService**</span><span class="sxs-lookup"><span data-stu-id="d7069-137">Allowed values are: **Anonymous**, **Username**, **UsernameAndPassword**, **WindowsAzureHDInsightService**</span></span> | <span data-ttu-id="d7069-138">Yes</span><span class="sxs-lookup"><span data-stu-id="d7069-138">Yes</span></span> |
| <span data-ttu-id="d7069-139">serviceDiscoveryMode</span><span class="sxs-lookup"><span data-stu-id="d7069-139">serviceDiscoveryMode</span></span> | <span data-ttu-id="d7069-140">true to indicate using the ZooKeeper service, false not.</span><span class="sxs-lookup"><span data-stu-id="d7069-140">true to indicate using the ZooKeeper service, false not.</span></span>  | <span data-ttu-id="d7069-141">No</span><span class="sxs-lookup"><span data-stu-id="d7069-141">No</span></span> |
| <span data-ttu-id="d7069-142">zooKeeperNameSpace</span><span class="sxs-lookup"><span data-stu-id="d7069-142">zooKeeperNameSpace</span></span> | <span data-ttu-id="d7069-143">The namespace on ZooKeeper under which Hive Server 2 nodes are added.</span><span class="sxs-lookup"><span data-stu-id="d7069-143">The namespace on ZooKeeper under which Hive Server 2 nodes are added.</span></span>  | <span data-ttu-id="d7069-144">No</span><span class="sxs-lookup"><span data-stu-id="d7069-144">No</span></span> |
| <span data-ttu-id="d7069-145">useNativeQuery</span><span class="sxs-lookup"><span data-stu-id="d7069-145">useNativeQuery</span></span> | <span data-ttu-id="d7069-146">Specifies whether the driver uses native HiveQL queries,or converts them into an equivalent form in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d7069-146">Specifies whether the driver uses native HiveQL queries,or converts them into an equivalent form in HiveQL.</span></span>  | <span data-ttu-id="d7069-147">No</span><span class="sxs-lookup"><span data-stu-id="d7069-147">No</span></span> |
| <span data-ttu-id="d7069-148">username</span><span class="sxs-lookup"><span data-stu-id="d7069-148">username</span></span> | <span data-ttu-id="d7069-149">The user name that you use to access Hive Server.</span><span class="sxs-lookup"><span data-stu-id="d7069-149">The user name that you use to access Hive Server.</span></span>  | <span data-ttu-id="d7069-150">No</span><span class="sxs-lookup"><span data-stu-id="d7069-150">No</span></span> |
| <span data-ttu-id="d7069-151">password</span><span class="sxs-lookup"><span data-stu-id="d7069-151">password</span></span> | <span data-ttu-id="d7069-152">The password corresponding to the user.</span><span class="sxs-lookup"><span data-stu-id="d7069-152">The password corresponding to the user.</span></span> <span data-ttu-id="d7069-153">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d7069-153">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="d7069-154">No</span><span class="sxs-lookup"><span data-stu-id="d7069-154">No</span></span> |
| <span data-ttu-id="d7069-155">httpPath</span><span class="sxs-lookup"><span data-stu-id="d7069-155">httpPath</span></span> | <span data-ttu-id="d7069-156">The partial URL corresponding to the Hive server.</span><span class="sxs-lookup"><span data-stu-id="d7069-156">The partial URL corresponding to the Hive server.</span></span>  | <span data-ttu-id="d7069-157">No</span><span class="sxs-lookup"><span data-stu-id="d7069-157">No</span></span> |
| <span data-ttu-id="d7069-158">enableSsl</span><span class="sxs-lookup"><span data-stu-id="d7069-158">enableSsl</span></span> | <span data-ttu-id="d7069-159">Specifies whether the connections to the server are encrypted using SSL.</span><span class="sxs-lookup"><span data-stu-id="d7069-159">Specifies whether the connections to the server are encrypted using SSL.</span></span> <span data-ttu-id="d7069-160">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="d7069-160">The default value is false.</span></span>  | <span data-ttu-id="d7069-161">No</span><span class="sxs-lookup"><span data-stu-id="d7069-161">No</span></span> |
| <span data-ttu-id="d7069-162">trustedCertPath</span><span class="sxs-lookup"><span data-stu-id="d7069-162">trustedCertPath</span></span> | <span data-ttu-id="d7069-163">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="d7069-163">The full path of the .pem file containing trusted CA certificates for verifying the server when connecting over SSL.</span></span> <span data-ttu-id="d7069-164">This property can only be set when using SSL on self-hosted IR.</span><span class="sxs-lookup"><span data-stu-id="d7069-164">This property can only be set when using SSL on self-hosted IR.</span></span> <span data-ttu-id="d7069-165">The default value is the cacerts.pem file installed with the IR.</span><span class="sxs-lookup"><span data-stu-id="d7069-165">The default value is the cacerts.pem file installed with the IR.</span></span>  | <span data-ttu-id="d7069-166">No</span><span class="sxs-lookup"><span data-stu-id="d7069-166">No</span></span> |
| <span data-ttu-id="d7069-167">useSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="d7069-167">useSystemTrustStore</span></span> | <span data-ttu-id="d7069-168">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span><span class="sxs-lookup"><span data-stu-id="d7069-168">Specifies whether to use a CA certificate from the system trust store or from a specified PEM file.</span></span> <span data-ttu-id="d7069-169">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="d7069-169">The default value is false.</span></span>  | <span data-ttu-id="d7069-170">No</span><span class="sxs-lookup"><span data-stu-id="d7069-170">No</span></span> |
| <span data-ttu-id="d7069-171">allowHostNameCNMismatch</span><span class="sxs-lookup"><span data-stu-id="d7069-171">allowHostNameCNMismatch</span></span> | <span data-ttu-id="d7069-172">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span><span class="sxs-lookup"><span data-stu-id="d7069-172">Specifies whether to require a CA-issued SSL certificate name to match the host name of the server when connecting over SSL.</span></span> <span data-ttu-id="d7069-173">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="d7069-173">The default value is false.</span></span>  | <span data-ttu-id="d7069-174">No</span><span class="sxs-lookup"><span data-stu-id="d7069-174">No</span></span> |
| <span data-ttu-id="d7069-175">allowSelfSignedServerCert</span><span class="sxs-lookup"><span data-stu-id="d7069-175">allowSelfSignedServerCert</span></span> | <span data-ttu-id="d7069-176">Specifies whether to allow self-signed certificates from the server.</span><span class="sxs-lookup"><span data-stu-id="d7069-176">Specifies whether to allow self-signed certificates from the server.</span></span> <span data-ttu-id="d7069-177">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="d7069-177">The default value is false.</span></span>  | <span data-ttu-id="d7069-178">No</span><span class="sxs-lookup"><span data-stu-id="d7069-178">No</span></span> |
| <span data-ttu-id="d7069-179">connectVia</span><span class="sxs-lookup"><span data-stu-id="d7069-179">connectVia</span></span> | <span data-ttu-id="d7069-180">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="d7069-180">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="d7069-181">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="d7069-181">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="d7069-182">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d7069-182">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="d7069-183">No</span><span class="sxs-lookup"><span data-stu-id="d7069-183">No</span></span> |

<span data-ttu-id="d7069-184">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d7069-184">**Example:**</span></span>

```json
{
    "name": "HiveLinkedService",
    "properties": {
        "type": "Hive",
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

## <a name="dataset-properties"></a><span data-ttu-id="d7069-185">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="d7069-185">Dataset properties</span></span>

<span data-ttu-id="d7069-186">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="d7069-186">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="d7069-187">This section provides a list of properties supported by Hive dataset.</span><span class="sxs-lookup"><span data-stu-id="d7069-187">This section provides a list of properties supported by Hive dataset.</span></span>

<span data-ttu-id="d7069-188">To copy data from Hive, set the type property of the dataset to **HiveObject**.</span><span class="sxs-lookup"><span data-stu-id="d7069-188">To copy data from Hive, set the type property of the dataset to **HiveObject**.</span></span> <span data-ttu-id="d7069-189">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="d7069-189">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="d7069-190">**Example**</span><span class="sxs-lookup"><span data-stu-id="d7069-190">**Example**</span></span>

```json
{
    "name": "HiveDataset",
    "properties": {
        "type": "HiveObject",
        "linkedServiceName": {
            "referenceName": "<Hive linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="d7069-191">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="d7069-191">Copy activity properties</span></span>

<span data-ttu-id="d7069-192">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="d7069-192">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="d7069-193">This section provides a list of properties supported by Hive source.</span><span class="sxs-lookup"><span data-stu-id="d7069-193">This section provides a list of properties supported by Hive source.</span></span>

### <a name="hivesource-as-source"></a><span data-ttu-id="d7069-194">HiveSource as source</span><span class="sxs-lookup"><span data-stu-id="d7069-194">HiveSource as source</span></span>

<span data-ttu-id="d7069-195">To copy data from Hive, set the source type in the copy activity to **HiveSource**.</span><span class="sxs-lookup"><span data-stu-id="d7069-195">To copy data from Hive, set the source type in the copy activity to **HiveSource**.</span></span> <span data-ttu-id="d7069-196">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="d7069-196">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="d7069-197">Property</span><span class="sxs-lookup"><span data-stu-id="d7069-197">Property</span></span> | <span data-ttu-id="d7069-198">Description</span><span class="sxs-lookup"><span data-stu-id="d7069-198">Description</span></span> | <span data-ttu-id="d7069-199">Required</span><span class="sxs-lookup"><span data-stu-id="d7069-199">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d7069-200">type</span><span class="sxs-lookup"><span data-stu-id="d7069-200">type</span></span> | <span data-ttu-id="d7069-201">The type property of the copy activity source must be set to: **HiveSource**</span><span class="sxs-lookup"><span data-stu-id="d7069-201">The type property of the copy activity source must be set to: **HiveSource**</span></span> | <span data-ttu-id="d7069-202">Yes</span><span class="sxs-lookup"><span data-stu-id="d7069-202">Yes</span></span> |
| <span data-ttu-id="d7069-203">query</span><span class="sxs-lookup"><span data-stu-id="d7069-203">query</span></span> | <span data-ttu-id="d7069-204">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="d7069-204">Use the custom SQL query to read data.</span></span> <span data-ttu-id="d7069-205">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="d7069-205">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="d7069-206">Yes</span><span class="sxs-lookup"><span data-stu-id="d7069-206">Yes</span></span> |

<span data-ttu-id="d7069-207">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d7069-207">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromHive",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Hive input dataset name>",
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
                "type": "HiveSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="d7069-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7069-208">Next steps</span></span>
<span data-ttu-id="d7069-209">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d7069-209">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
